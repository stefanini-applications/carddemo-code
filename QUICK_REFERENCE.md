# CardDemo Core-Application - Quick Reference Guide

## Key Files & Locations

### Entry Points
- **Sign-In:** COSGN00C.cbl (TRANID: CC00)
- **Main Menu:** COMEN01C.cbl (TRANID: CM00)
- **Admin Menu:** COADM01C.cbl (TRANID: CA00)

### Master Data Copybooks
| File | Record Type | Size | Key |
|------|-------------|------|-----|
| CVCUS01Y.cpy | CUSTOMER-RECORD | 500B | CUST-ID (9 digits) |
| CVACT01Y.cpy | ACCOUNT-RECORD | 300B | ACCT-ID (11 digits) |
| CVTRA05Y.cpy | TRAN-RECORD | 350B | TRAN-ID (16 chars) |
| CVACT03Y.cpy | CARD-XREF-RECORD | 50B | CARD-NUM (16 chars) |

### Primary VSAM Datasets
- AWS.M2.CARDDEMO.ACCTDATA.VSAM.KSDS (Accounts)
- AWS.M2.CARDDEMO.TRANSACT.VSAM.KSDS (Transactions)
- AWS.M2.CARDDEMO.CCXREF.VSAM.KSDS (Card cross-reference)
- AWS.M2.CARDDEMO.CUSTDATA.VSAM.KSDS (Customers)
- AWS.M2.CARDDEMO.USRSEC.VSAM.KSDS (User authentication)

### Batch Jobs
```
POSTTRAN.jcl      → Process daily transactions (CBTRN02C)
CREASTMT.jcl      → Generate statements (CBSTM03A)
TRANIDX.jcl       → Build alternate index on TRANSACT
ACCTFILE.jcl      → Load account master
TRANBKP.jcl       → Backup & redefine transaction file
OPENFIL.jcl       → Open CICS file resources
```

### Automation Scripts
```bash
./scripts/run_full_batch.sh    # 16-step nightly orchestration
./scripts/run_posting.sh        # 7-step core posting workflow
./scripts/local_compile.sh      # Compile COBOL locally (GnuCOBOL)
./scripts/remote_compile.sh     # Compile on mainframe
```

---

## Common Tasks

### View Account Information
1. Sign in with COSGN00C (TRANID: CC00)
   - User: ADMIN001 or USER0001
   - Password: PASSWORD
2. Select option from COMEN01C menu (TRANID: CM00)
3. Choose COACTVWC (TRANID: CAVW) to view account details
4. Enter account ID → displays balance, limits, status, dates

### Add a Transaction
1. From COMEN01C (TRANID: CM00), select transaction option
2. COTRN02C (TRANID: CT02) - Add new transaction
3. Enter card number, amount, merchant, description
4. System generates unique TRAN-ID, validates card/account via CCXREF
5. Updates account balance, writes to TRANSACT file

### Process Daily Batch
```bash
cd /tmp/workspace-module-detail/repo
./scripts/run_posting.sh
```
Processes daily transactions through:
1. CLOSEFIL.jcl → ACCTFILE → TCATBALF → TRANBKP
2. POSTTRAN.jcl (CBTRN02C) → Process DALYTRAN
3. TRANIDX.jcl → Rebuild indexes
4. OPENFIL.jcl → Reopen files

---

## File Access Patterns

### Read Account
```cobol
EXEC CICS READ
    FILE('ACCTDAT')
    INTO(ACCOUNT-RECORD)
    RIDFLD(ACCT-ID)
    RESP(WS-RESP-CD)
END-EXEC
```

### Write New Transaction
```cobol
MOVE 'GENERATED-ID-16CHARS' TO TRAN-ID
EXEC CICS WRITE
    FILE('TRANSACT')
    FROM(TRAN-RECORD)
    RIDFLD(TRAN-ID)
    RESP(WS-RESP-CD)
END-EXEC
```

### Update Account Balance
```cobol
EXEC CICS READ
    FILE('ACCTDAT')
    INTO(ACCOUNT-RECORD)
    RIDFLD(ACCT-ID)
    RESP(WS-RESP-CD)
END-EXEC
COMPUTE ACCT-CURR-BAL = ACCT-CURR-BAL - PAYMENT-AMT
EXEC CICS REWRITE
    FILE('ACCTDAT')
    FROM(ACCOUNT-RECORD)
    RESP(WS-RESP-CD)
END-EXEC
```

---

## Error Response Codes

| Code | Meaning | Action |
|------|---------|--------|
| DFHRESP(NORMAL) | Success | Continue |
| DFHRESP(NOTFND) | Record not found | Display error, re-prompt |
| DFHRESP(DUPREC) | Duplicate key | Reject insert, show error |
| DFHRESP(IOERR) | I/O error | Log error, alert operator |
| DFHRESP(NOTOPEN) | File not open | Run OPENFIL.jcl |

---

## Test Credentials

| User ID | Password | Role |
|---------|----------|------|
| ADMIN001 | PASSWORD | Administrator (access to CA00) |
| USER0001 | PASSWORD | Regular user (access to CM00) |

---

## Performance Targets

- CICS interactive response: <2.5 seconds (95th percentile)
- VSAM read (cache hit): <500ms
- VSAM write (with index update): <1s
- Full batch window: 2.5-3 hours
- TRANIDX (BLDINDEX): 60-90 seconds

---

## Emergency Procedures

### Files Corrupted
1. Stop CICS
2. `DELETE AWS.M2.CARDDEMO.TRANSACT.VSAM.KSDS CLUSTER`
3. Run TRANBKP.jcl to restore from backup
4. Run TRANIDX.jcl to rebuild AIX
5. Run OPENFIL.jcl to reopen files

### Batch Failed
- Check job output for CBTRN02C errors
- Verify DALYTRAN.PS contains valid data
- Run POSTTRAN.jcl again

### CICS File Not Open
- Run OPENFIL.jcl via JES
- Verify CEMT shows all files as OPEN

---

## Directory Map

```
repo/
├── app/
│   ├── cbl/              (29 COBOL programs)
│   ├── bms/              (17 BMS mapsets)
│   ├── cpy/              (30 copybooks)
│   ├── cpy-bms/          (18 BMS-generated copybooks)
│   ├── jcl/              (36 JCL jobs)
│   ├── data/             (ASCII/EBCDIC seed data)
│   └── [other dirs]
├── scripts/              (11 automation scripts)
├── docs/                 (architecture & overview)
├── README.md             (project intro)
├── CARDDEMO_ANALYSIS.md  (comprehensive analysis)
└── QUICK_REFERENCE.md    (this file)
```

---

## Key Metrics

- **Total COBOL LOC:** ~19,496
- **Total Copybooks:** 48 (30 data + 18 BMS)
- **Interactive Transactions:** 15+ CICS programs
- **Batch Jobs:** 36 JCL files
- **VSAM Files:** 7 main datasets
- **Record Sizes:** 50B-500B
- **Primary Index:** B-tree KSDS
- **Alternate Index:** TRANSACT by timestamp

---

## Support & Escalation

1. **Program Compilation Errors** → Check app/cbl/*.cbl copybook includes
2. **File Not Open** → Run OPENFIL.jcl
3. **Data Not Found** → Verify ACCTFILE/CUSTFILE/XREFFILE jobs completed
4. **Batch Job Failed** → Check job log for CBTRN02C program abend codes
5. **VSAM Corruption** → Follow Emergency Procedures above

---

**Last Updated:** 2024  
**Repository:** /tmp/workspace-module-detail/repo  
**Module:** core-application
