# Module File Map

<!-- MODULE_FILE_MAP_START -->
app/cbl/COSGN00C.cbl = authentication
app/bms/COSGN00.bms = authentication
app/cpy/CSUSR01Y.cpy = authentication, user-management

app/cbl/COACTVWC.cbl = account-management
app/cbl/COACTUPC.cbl = account-management
app/bms/COACTVW.bms = account-management
app/bms/COACTUP.bms = account-management
app/cpy/CVACT01Y.cpy = account-management, batch-processing
app/cpy/CVACT02Y.cpy = account-management, card-management
app/cpy/CVACT03Y.cpy = account-management

app/cbl/COCRDLIC.cbl = card-management
app/cbl/COCRDSLC.cbl = card-management
app/cbl/COCRDUPC.cbl = card-management
app/bms/COCRDLI.bms = card-management
app/bms/COCRDSL.bms = card-management
app/bms/COCRDUP.bms = card-management
app/cpy/CVCARD01Y.cpy = card-management

app/cbl/COTRN00C.cbl = transaction-management
app/cbl/COTRN01C.cbl = transaction-management
app/cbl/COTRN02C.cbl = transaction-management
app/bms/COTRN00.bms = transaction-management
app/bms/COTRN01.bms = transaction-management
app/bms/COTRN02.bms = transaction-management
app/cpy/CVTRA05Y.cpy = transaction-management, batch-processing
app/cpy/CVTRA01Y.cpy = transaction-management, batch-processing
app/cpy/CVTRA02Y.cpy = transaction-management, batch-processing
app/cpy/CVTRA03Y.cpy = transaction-management, batch-processing
app/cpy/CVTRA04Y.cpy = transaction-management, batch-processing

app/cbl/CORPT00C.cbl = reports
app/bms/CORPT00.bms = reports

app/cbl/COBIL00C.cbl = bill-payment
app/bms/COBIL00.bms = bill-payment

app/cbl/COUSR00C.cbl = user-management
app/cbl/COUSR01C.cbl = user-management
app/cbl/COUSR02C.cbl = user-management
app/cbl/COUSR03C.cbl = user-management
app/bms/COUSR00.bms = user-management
app/bms/COUSR01.bms = user-management
app/bms/COUSR02.bms = user-management
app/bms/COUSR03.bms = user-management

app/cbl/COMEN01C.cbl = authentication, account-management, card-management, transaction-management, reports, bill-payment, user-management
app/bms/COMEN01.bms = authentication, account-management, card-management, transaction-management, reports, bill-payment, user-management
app/cbl/COADM01C.cbl = user-management, transaction-types
app/bms/COADM01.bms = user-management, transaction-types

app/cbl/CBTRN01C.cbl = batch-processing
app/cbl/CBTRN02C.cbl = batch-processing
app/cbl/CBTRN03C.cbl = batch-processing
app/cbl/CBSTM01B.cbl = batch-processing
app/cbl/CBSTM01C.cbl = batch-processing
app/cbl/CBACT01C.cbl = batch-processing, account-management
app/cbl/CBACT02C.cbl = batch-processing, account-management
app/cbl/CBACT03C.cbl = batch-processing, account-management
app/cbl/CBACT04C.cbl = batch-processing, account-management
app/cbl/CBCUS01C.cbl = batch-processing
app/cbl/LNKBILI.cbl = batch-processing, bill-payment
app/cbl/LNKLBIL.cbl = batch-processing, bill-payment
app/jcl/POSTTRAN.jcl = batch-processing
app/jcl/INTCALC.jcl = batch-processing
app/jcl/CREASTMT.jcl = batch-processing
app/jcl/COMBTRAN.jcl = batch-processing
app/jcl/ACCTFILE.jcl = batch-processing, account-management
app/jcl/CARDFILE.jcl = batch-processing, card-management
app/jcl/CUSTFILE.jcl = batch-processing
app/jcl/XREFFILE.jcl = batch-processing, card-management
app/jcl/TRANFILE.jcl = batch-processing, transaction-management
app/jcl/DUSRSECJ.jcl = batch-processing, authentication, user-management
app/jcl/OPENFILE.jcl = batch-processing
app/jcl/CLOSEFIL.jcl = batch-processing
app/jcl/TRANIDX.jcl = batch-processing, card-management

app/app-authorization-ims-db2-mq/** = authorization
app/app-authorization-ims-db2-mq/cbl/COPAUA0C.cbl = authorization
app/app-authorization-ims-db2-mq/cbl/COPAUA1C.cbl = authorization
app/app-authorization-ims-db2-mq/cbl/COPAUS0C.cbl = authorization
app/app-authorization-ims-db2-mq/cbl/COPAUS1C.cbl = authorization
app/app-authorization-ims-db2-mq/bms/COPAU00.bms = authorization
app/app-authorization-ims-db2-mq/bms/COPAU01.bms = authorization
app/app-authorization-ims-db2-mq/cpy/CCPAURQY.cpy = authorization
app/app-authorization-ims-db2-mq/cpy/CIPAUSMY.cpy = authorization
app/app-authorization-ims-db2-mq/ddl/AUTHFRDS.ddl = authorization
app/app-authorization-ims-db2-mq/ims/** = authorization
app/app-authorization-ims-db2-mq/jcl/** = authorization
app/app-vsam-mq/cbl/CODATE01.cbl = authorization
app/app-vsam-mq/cbl/COACCT01.cbl = authorization, account-management
app/app-vsam-mq/** = authorization

app/app-transaction-type-db2/cbl/COTRTLIC.cbl = transaction-types
app/app-transaction-type-db2/cbl/COTRTUPC.cbl = transaction-types
app/app-transaction-type-db2/bms/COTRTLI.bms = transaction-types
app/app-transaction-type-db2/bms/COTRTUP.bms = transaction-types
app/app-transaction-type-db2/ddl/TRNTYPE.ddl = transaction-types
app/app-transaction-type-db2/ddl/TRNTYCAT.ddl = transaction-types
app/app-transaction-type-db2/dcl/DCLTRTYP.dcl = transaction-types
app/app-transaction-type-db2/dcl/DCLTRCAT.dcl = transaction-types
app/app-transaction-type-db2/jcl/** = transaction-types

app/cpy/COCOM01Y.cpy = authentication, account-management, card-management, transaction-management, reports, bill-payment, user-management
app/cpy/COTTLY01Y.cpy = transaction-management, transaction-types
app/cpy/CVCUS01Y.cpy = account-management, batch-processing
app/cpy/CVCARD01Y.cpy = card-management
app/cpy/CVCRD01Y.cpy = card-management
app/cpy/CVDTT01Y.cpy = authentication, account-management, card-management, transaction-management
app/cpy/CSMSG01Y.cpy = authentication, account-management, card-management, transaction-management, reports, bill-payment, user-management
app/cpy/CSFLD01Y.cpy = authentication, account-management, card-management, transaction-management

app/asm/MVSWAIT.asm = batch-processing
app/asm/COBDATFT.asm = batch-processing, account-management, card-management, transaction-management

app/csd/** = authentication, account-management, card-management, transaction-management, reports, bill-payment, user-management, batch-processing
app/data/** = batch-processing
<!-- MODULE_FILE_MAP_END -->
