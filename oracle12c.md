# New Features of Oracle Database 12c 

## Enterprise Manager and Other Tools  [1] 
- Use EM Express 
- Use OUI, DBCA for installation and configuration 

## Basics of Multitenant Container Database (CDB)  [2] 
- Identify the benefits of the multitenant container database 
- Explain root and multitenant architecture 

## Configuring and Creating CDBs and PDBs [2] 
- Create and configure a CDB 
- Create and configure a PDB 
- Migrate a non-CDB to a PDB database 

## Managing CDBs and PDBs  [3] 
- Establish connection to a CDB/PDB 
- Start up and shut down a CDB/PDB 
- Change instance parameters for a CDB/PDB 

## Managing Tablespaces, Common and Local Users, Privileges and Roles  [3] 
- Manage tablespaces in a CDB/PDB 
- Manage users and privileges for CDB/PDB 

## Backup, Recovery and Flashback for a CDB/PDB  [7] 
- Perform backup of CDB and PDB 
- Perform recovery of CDB and PDB 
- Perform Flashback for a CDB 

## Information Lifecycle Management and Storage Enhancements  [9] 
- Use ILM features 
- Perform tracking and automated data placement 
- Move a data file online 

## In-Database Archiving and Valid-Time Temporal  [9] 
- Differentiate between ILM and Valid-Time Temporal 
- Set and use Valid Time Temporal 
- Use In-Database archiving 

## Auditing  [4] 
- Enable and configure Unified Audit Data Trail 
- Create and enable audit policies 

## Privileges [4] 
- Use administrative privileges 
- Create, enable and use privilege analysis 

## Oracle Data Redaction  [4] 
- Use and manage Oracle Data Redaction policies 

## RMAN and Flashback Data Archive [7] 
- Use RMAN enhancements 
- Implement the new features in Flashback Data Archive 

## Real-Time Database Operation Monitoring [1] 
- Implement real-time database operation monitoring 

## SQL Tuning  [5] 
- Use Adaptive Execution Plans 
- Use enhanced features of statistics gathering 
- Use Adaptive SQL Plan Management 

## Emergency Monitoring, Real-Time ADDM, Compare Period ADDM, and Active Session History (ASH) Analytics  [1] 
- Perform emergency monitoring and real-time ADDM 
- Generate ADDM Compare Period 
- Diagnose performance issues using ASH enhancements 

## Resource Manager and Other Performance Enhancements  [6] 
- Use Resource Manager for a CDB and PDB 
- Explain Multi-process Multi-threaded Oracle architecture 
- Use Flash Cache 

## Index and Table Enhancements  [6] 
- Use Index enhancements 
- Use Table enhancements 
- Use Online operation enhancements 

## ADR and Network Enhancements  [1] 
- Explain ADR enhancements 

## Oracle Data Pump, SQL*Loader, External Tables and Online Operations Enhancements [8]
- Use Oracle Data Pump enhancements 
- Use SQL*Loader and External table enhancements 

## Partitioning Enhancements  [8] 
- Explain Partitioning enhancements 
- Explain Index enhancements for partitioned tables 

## SQL Enhancements  [6] 
- Use Oracle Database Migration Assistant for Unicode 
- Use Row limiting clause, and secure file LOBs enhancements 
- Configure extended datatypes 


# Key DBA Skills 

## Core Administration 
- Explain the fundamentals of DB architecture 
- Install and configure a database 
- Configure server and client network for a database 
- Monitor database alerts 
- Perform daily administration tasks 
- Apply and review patches 
- Back up and recover the database 
- Troubleshoot network and database issues 
- Detect and repair data failures with Data Recovery Advisor 
- Implement Flashback Technology 
- Load and Unload Data 
- Miscellaneous
    - Relocate SYSAUX occupants 
    - Create a default permanent tablespace 
    - Use the Redo Logfile Size Advisor 
    - Use Secure File LOBs 
    - Use Direct NFS 

## Performance Management 
- Design the database layout for optimal performance 
- Monitor performace 
- Manage memory 
- Analyze and identify performance issues 
- Perform real application testing 
- Use Resource Manager to manage resources 
- Implement Application Tuning 

## Storage 
- Manage database structures 
- Administer ASM 
- Manage ASM disks and diskgroups 
- Manage ASM instance 
- Manage VLDB 
- Implement Space Management 

## Security 
- Develop and implement a security policy 
- Configure and manage auditing 
- Create the password file 
- Implement column and tablespace encryption 

----

## Enterprise Manager and Other Tools

### Use EM Express 
### Use OUI, DBCA for installation and configuration

- Require: 
    - Init parameter DISPATCHERS: minimum value 1
    - EM Express requires Oracle XML DB components installed
        - automatically when you install Oracle Database 12c
- Lightweight. Available only when DB is open.
- Configure either HTTP or HTTPS port:
    - DBMS_XDDB_CONFIG.setHTTPsPort(5500);
    - https://localhost.localdomain:5500/em
    - DBMS_XDDB_CONFIG.setHTTPPort(5500);
    - http://localhost.localdomain:5500/em
    - select DBMS_XDDB_CONFIG.getHTTPPort from dual
    - select DBMS_XDDB_CONFIG.getHTTPsPort from dual
- Must define different port for each instance. 
    - Cannot share port. Cannot see other instance in RAC.
- Roles: 
    - EM_EXPRESS_BASIC : read-only, include SELECT_CATALOG_ROLE
    - EM_EXPRESS_ALL : All EM Express functions
- Unable to: 
    - Cannot start/stop instance
    - Cannot perform any action to change database state
    - Alternative: Enterprise Manager Cloud Control 12c
- Display
    - Home Page:
        - Incident: Last 24 Hours
        - Performance
        - Resources
        - SQL Monitor
    - Menus
        - Configuration: Init parameters, Memory, DB feature usage, DB properties
        - Storage: Control files, Tablespaces, Undo tablespaces, Redo and archived redo logs
        - Security: Users, Roles, Profiles
        - Performance: Performance Hub, SQL Tuning Advisor
- DBCA new feature:
    - Create, Delete, Unplug PDB
    - Enable EM Express port
- SQL Developer
    - DBA connected need to use features
    - DB start/ stop
    - DB Configuration
    - Data Pump export/ import
    - RMAN backup/ recovery
    - Security config: Users, Roles, Profiles
    - Storage config: Tablespaces, Undo tablespaces, Redo and archived redo logs

## Real-Time Database Operation Monitoring
### Implement real-time database operation monitoring

- Aim and Use: 
    - Find resource instensive (expensive) code
    - Monitor concurrent jobs and check progress
    - Analyze offline
- Superset of 11g features:
    - Real-Time SQL Monitor
    - Active Session History (ASH)
    - SQL Trace
    - DBMS_MONITOR
- Require: 
    - License: Oracle's SQL Tuning Pack
    - Parameter: CONTROL_MANAGEMENT_PACK_ACCESS=DIAGNOSTIC+TUNING
    - Parameter: STATISTICS_LEVEL=ALL or TYPICAL (default)
- Concept: database operation and idle time
    1. Simple database operation: One or multiple SQL or PL/SQL executed in a _single Session_
    1. Composite database operation: SQL or PL/SQL executed executed within a _time interval_
        - Multiple session: Single operation executed _concurrently_ 
        - Single session: Only one session is executing _at any given time_. Can be one or more session.
    - Idle time= Time for a session without executing SQL or PL/SQL
    - Identifier: database operation name, database operation execution ID
- Help DBA to:
    - Monitor jobs: Alert DBA when job exceed set time.
    - Diagnosis: Identify expensive statements in database operation
    - Compare: Compare current and previous executions
    - Compare: Compare executions after database upgrades
- Monitored data in V$SQL_MONITOR:
    - SQL_EXEC_ID: database operation execution ID, PK
    - SQL_EXEC_START: start timestamp
    - SQL_ID: refer V$SQL
- Specify database operation in two ways:
    - Always name the operation. Time of start and end of operation gathered explicitly or implicitly
        - Recommended naming to avoid collision: <component>.<sub_component>.<operation_name>
    - Tagging. Java or OCI application:
        - Environment variable: ORA_DBOP, or
        - JDBC 4.1: setClientInfo, or
        - Oracle Call Interface (OCI): OCIAttrSet and OCIAppCtxSet
    - Bracketing. Within PL/SQL: Specify begin and end of operation
        - Procedure: BEGIN_OPERATION and END_OPERATION of DBMS_SQL_MONITOR package
        - Argument: set FORCED_TRACKING := 'Y' to force all SQL to be tracked
        - Default: Track operation only when it is expensive
            - Expensive threshold: SQL takes 5 seconds in CPU or CPU, or run in parallel
    - SQL: Hint: MONITOR and NO_MONITOR
- Control
    - OEM Cloud Control: Performance Menu
    - EM Database Express: SQL Monitor Menu
- DBA views on current monitoring:
    - V$SQL_MONITOR: SQL monitored
    - V$SQL_MONITOR_SESSTAT: used by report generator. Use V$SESSTAT instead instead
    - V$SQL_PLAN_MONITOR
    - Existing Views: V$ACTIVE_SESSION_HISTORY, V$SESSION, V$SESSION_LONGOPS, V$SQL, V$SQL_PLAN
- DBA views on completed monitoring:
    - DBA_HIST_REPORTS
    - DBA_HIST_REPORTS_DETAILS
    - DBA_HIST_ACTIVE_SESS_HISTORY
- Show monitor Report
    - select DBMS_SQL_MONITOR.REPORT_SQL_MONITOR_LIST_XML() from dual;

## Emergency Monitoring, Real-Time ADDM, Compare Period ADDM, and Active Session History (ASH) Analytics
### Perform emergency monitoring and real-time ADDM 

- Aim and Use of Emergency Monitoring
    - Use case: Production perfromance emergency
    - Not good to run performance diagnosis: too resource intensive
    - Shutdown is last resort
    - Need a tool for lightweight analysis
- Require:
    - 11g: require "memory access mode"
    - 12c: no requirement. No collector process.
- Monitoring Data
    - Active Session History (ASH) buffers
        - Real time performance data of last 60 minutes
        - but depends on level of instance activity and resource contention
    - Hang analysis
        - pinpoint blocking session
        - kill the root blocker
- Limitation
    - Not always successful: Need to shutdown as last resort
    - Cannot identify root cause

- Aim of Real-Time ADDM (Automatic Database Diagnostic Monitor)
    - Identify root cause of emergency
    - Not normal ADDM
- Monitoring Data
    - Active Session History (ASH) from SGA, gathered by process MMON 
    - Also available in RAC
        - Collect SGA data from each instance, bypass SQL Retrieval Layer
    - Store in Automatic Workload Repository (AWR)
        - High Load: Average Active Session >= 3 * nbr of CPU core
        - I/O: Active sessions impacted by I/O
        - CPU: Active sessions >= 10% of total load, or CPU usage >= 50%
        - Hung sessions: 10% of sessions are hung
    - Within 5 min of report generation, another report is not created
    - Within 45 min of report generation, another report is created only on impact of 100% or higher
- Views:
    - DBA_HIST_REPORTS
    - DBA_HIST_REPORTS_DETAILS
- Access:
    - select DBMS_ADDM.REAL_TIME_ADDM_REPORT() from dual
    - EM Database Express: Performance Menu
    - EM Cloud Control 12c: Top Activity Snapshot
- Connection: Normal Mode and Diagnostic Mode
    - Normal Mode: 
    - Diagnostic Mode: Latch-less

- Combine Emergency Monitoring and Real-Time ADDM
    - On slowdown: Use Emergency Monitoring first
    - Real-Time ADDM for:
        - Root cause analysis
        - Obtain recommendations to fix problems

### Generate ADDM Compare Period Report

- Aim and Use of ADDM Compare Period Report
    - Analyze performance degradation
    - Compare a "bad" time period vs a "good" baseline period
- AWR comparsion is not good enough because:
    - manual comparsion of AWR statistics is tedious and error-prone
    - Compare among preseved snapshots
        - or Compare DB Replay Capture
    - Isolate root causes of performance differentials
    - Do not map root cause to performance change
    - Output: text or html
- Methodology of ADDM Compare Period Report
    - Find potential causes
    - Run ADDM analysis. Accept DB Replay.
    - map system changes to performance differentials
        - but do not know why performance changed
    - Can use Real Application Testing
    - Output: CPU, memory, I/O, interconnect (in RAC)
- SQL Commonality
    - 100 percent scale of Similarity of SQL statements, workloads and statements
    - Higher commonality: means comparsion is more reliable, such as 80-90 percent
    - Do not rely on comparsion with commonality less than 80 percent
- EM Cloud Control 12c
    - Select a period of poor performance: Start and End Time
    - Select a baseline to represent a good performance
        1. Manual choose a recent snapshot offset
        1. system_moving_window baseline
        1. Customized time without regard of snapshot or baseline
    - Run Comparsion report
- By DBMS_ADDM package
    - COMPARE_INSTANCES: two time periods over single/ multiple instance
    - COMPARE_DATABASES: two time periods over single/ multiple database
    - COMPARE_CAPTURE_REPLAY_REPORT: compare workload capture vs its replay
    - COMPARE_REPLAY_REPLAY_REPORT: compare replay vs another replay

### Diagnose performance issues using ASH enhancements 

- Enhancements: Automatic Session History (ASH) in EM Cloud Control 12c
    - Filtering dimension
    - Drilling down
- Enhancements: Automatic Diagnostic Repository (ADR)
    - file based repository under ADR directory
    - DDL logging
        - Require: Oracle Change Management Pack
        - Parameter: enable_ddl_logging= true | false
        - 12c: exclusive file "$ADR_HOME/log/ddl/log,xml" instead of alert log
        - Same format as alert.log
        - (!) SQL command: SHOW LOG
    - Debug log
        - Under "$ADR_HOME/log/debug/"
        - Describe unusual events
        - Aid Oracle Support personnel. Not for DBA.
- Enhancements: Network
    - Network Compression added to Advanced Compression Option
    - File "sqlnet.ora"
        - SQLNET.COMPRESSION= ON | OFF (default)
        - SQLNET.COMPRESSION_LEVEL= LOW | HIGH
        - SQLNET.COMPRESSION_THRESHOLD= default 1024 bytes: min size of compression
    - Parameter: DEFAULT_SDU_SIZE
        - Can be set at "sqlnet.ora"
        - No need to change for very fast network
        - No need to change for application conveying only small network packets
        - Default 8KB. Max 2MB (original 64KB). Need more memory to increase it.

## Basics of Multitenant Container Database (CDB)

### Identify the benefits of the multitenant container database 

- Concept:
    - Non-CDB: pre-12c DB architecture
    - Single-tenant: One CDB+seed DB and One PDB
    - Multitenant: One CDB+seed DB. Any number of PDB
        - Require: Oracle Multitenant Option
- Benefit of Multitenant:
    - Lower cost: Less server and storage
    - Easy provisioning: No application change
    - Fast upgrade and patching: Upgrade/ Patch done in CDB applies to PDB
    - Central Management: Backup and Recovery can be done in CDB only
    - Performance Tuning: Tune Single SGA and PGA.
        - But need to manage PDB on sharing resources
    - Separation of duty: User of PDB is restricted to that PDB
    - Isolation of application: Application normally cannot be isolated without Oracle database Vault
- Fully backward Compatibile to non-CDB
- Instance associated to CDB (or non-CDB)

### Explain root and multitenant architecture

- Container database (CDB)
    - Has the root database, seed database and any PDB
    - PK: Container ID (CON_ID), Container Name (CON_NAME)
        - Administrator: CDBA
        - Background process
        - Memory
        - Control Files: Also govern PDBs
        - Oracle meteadata: Oracle supplied packages. Shared among PDBs
        - TEMP TS: Also as default TEMP TS. PDBs can have their own TEMP TS
        - UNDO TS: exclusive in CDB
        - Redo log: exclusive in CDB. Also archived redo log
        - CDB datafile: not assigned to PDBs
        - Resource Manager Plan: Share in whole CDB and PDB
- Root database
    - Oracle metadata
        - common users, role, profile: No local
        - Name: ROOT$CDB
- Seed database
    - Readonly template to create PDB
    - Cannot modify after creation
    - Special form of PDB but unusable
- Plugable database (PDB)
    - PK: Global Unique Identifer (GUID)
    - Max 252 PDBs
    - Full backward Compatibile to prior database release
        - Administrator: PDBA
        - PDB datafile: same as normal DB except UNDO
        - Application data TS
        - Local TEMP TS
        - Local user, role, profile
        - Local metadata: Located in SYSTEM and SYSAUX TS
        - PDB Resource Plan: Specific within PDB
- Shared Objects
    - Metadata links
        - dictionary objects in root container
        - Each PDB has a private data copy of the objects pointing to the metadata
    - Object-linked objects
        - DB link to access object of a PDB from another PDB
        - (!name) Data-linked objects
        - (!)
- Grant of Roles
    - Grant a common role to common user or role, commonly or locally
    - Grant a local role  to common user or role, only locally
    - Grant a local role  to local user or role , only locally

## Configuring and Creating CDBs and PDBs
### Create and configure a CDB 

- Tools to create DB
    - Create non-CDB same as in pre-12c, no change
    - Tools to create CDB: SQL*Plus, OUI, DBCA
    - Tools to create PDB: SQL*Plus, EM Cloud Control 12c, SQL Developer
    - EM Express cannot create CDB, PDB nor non-CDB
- Create CDB
    - Create Init file as usual
        - Only one SPFILE for each CDB. Each PDB may have their own init parameter sets.
        - ENABLE_PLUGGABLE_DATABASE= [true | false] to decide whether it is CDBs with PDBs.
        - Make sure directory specified in init file exists
            - ORA-27040: file create error...
        - DB_CREATE_FILE_DEST for root db. Use OMF otherwise
        - PDB_FILE_NAME_CONVERT for PDB. Use OMF otherwise
    - Create instance by START NOMOUNT
    - Create database
        - Add ENABLE_PLUGGABLE_DATABASE clause for CDBs+PDBs setting
        - SEED_FILE_NAME_CONVERT clause for files in seed db. Use OMF otherwise.
        - Order: 
            1. SEED_FILE_NAME_CONVERT clause in Create database
            2. OMF
            3. PDB_FILE_NAME_CONVERT init parameter
    - Close and Open seed DB
        - alter pluggable database pdb$seed close;
        - alter pluggable database pdb$seed open;
    - Create data dictionary by script such as:
        - @catalog.sql, @catblock.sql, @catproc.sql, @catoctk.sql, @owminst.sql, @pupbld.sql
    - Check V$CONTAINERS for created root and seed db. Check V$DATABASE for created CDB. (!)
    - At mount, create control files are created
    - At open, redo logs and datafiles of root db are created
- Create CDB by DBCA
    - "Advanced Mode"; then "Create a container database"
    - Last options of CDB creation at DBCA, specify
        - Default Permanent TS for root db; apart from SYSTEM and SYSAUX
        - Default TEMP TS for root db
        - Optionally create trigger to open all PDBs
        - Start Oracle listener
    - At minimum, create root database and seed db. Check V$CONTAINERS.
    - Services: Services created correspond to nbr of containers. View CDB_SERVICES
    - Predefined users with SYS and SYSTEM and, Predefined common roles

### Create and configure a PDB 

- Create PDB
    - By file copying
        - Create PDB from seed DB
        - Clone PDB to PDB
    - By a descriptor in XML file format
        - Plug a non-CDB to PDB
        - Unplug a PDB from another CDB and plug it to this CDB
- Create PDB from seed DB
    - CREATE PLUGABLE DATABASE pdb1
        - FILE_NAME_CONVERT clause (optional): Make sure directory specified exists
        - Admin user clause: `admin user uuu identified by ppp`
    - Created TS: SYSTEM, SYSAUX; User: SYS, SYSTEM; Default Service
    - PDB_DBA role create to user _uuu_
    - PDB_DBA role has connect privilege only. SYS need to grant privilege to PDB_DBA
    - Newly created PDB has status "NEW". No TS yet until open. Change to "NORMAL" after open PDB
    - PDB_TABLESPACE to check TS
- Clone PDB to PDB
    - Close and Reopen database to be cloned to readonly mode
        - ALTER PLUGGABLE DATABASE pdb2 close;
        - ALTER PLUGGABLE DATABASE pdb2 open read only;
    - CREATE PLUGABLE DATABASE pdb1 FROM pdb2
        - FILE_NAME_CONVERT clause (optional): Make sure directory specified exists
        - No admin user clause
    - Cannot clone from seed db
    - Can clone remote PDB (not same CDB) by DB link
        - SNAPSHOT COPY clause for supported target filesystem
- Plug a non-CDB to PDB by XML file in 12c (refer next section for other method)
    1. At non-CDB: open in read only mode. Close it first when needed.
    1. At non-CDB: exec DBMS_PDB.describe('orcl.xml');
    1. At CDB: exec DBMS_PDB.CHECK_PLUG_COMPATIBILITY(...);
    1. At CDB: CREATE PLUGGABLE DATABASE pdb1 USING 'orcl.xml' COPY FILE_NAME_CONVERT=(...);
        - NOCOPY: datafile in correct location
        - MOVE: move datafile to another location
        - COPY: copy datafile to another location (default)
    1. At CDB: @noncdb_to_pdb.sql
        - Remove uncessary metadata from SYSTEM TS
    1. Open PDB by: ALTER PLUGGABLE DATABASE pdb1 OPEN;
        - PDB status: "CONVERTING"
- Plug an unplgged PDB to CDB
    1. Close Source PDB， Unplug it
        - ALTER PLUGGABLE DATABASE pdb1 close;
        - ALTER PLUGGABLE DATABASE pdb1 UNPLUG INTO 'pdb1.xml';
        - STATUS changed to "UNUSABLE"
    1. Optional Drop Source PDB
        - DROP PLUGABLE DATABASE
            - "KEEP DATAFILE" by default. "INCLUDING DATAFILE" to drop files.
        - Must DROP it if it will plugged to same CDB later
    1. At target CDB check compatibility: exec DBMS_PDB.CHECK_PLUG_COMPATIBILITY(...);
    1. At target CDB: CREATE PLUGGABLE DATABASE pdb1 **AS CLONE** USING 'pdb1.xml' NOCOPY;
        - AS CLONE: datafile had not been created in this CDB (!)
- Create PDB by DBCA
    - from seed db, or by unplug/plug

### Migrate a non-CDB to a PDB database 
- Upgrading db to 12c is tedious. Below process do not need db upgrade.
- Export/Import Pump
    1. Create PDB from CDB
    1. expdp from source non-CDB
    1. impdp to PDB
- Export/import by transportable tablespace (TTS) or transportable database (TDB)
    1. Create PDB from CDB
    1. TTS or TDB export
    1. TTS or TDB import
- Replicate by Oracle Golden Gate
    1. Create PDB from CDB. Open PDB in read-write mode.
    1. Config: Unidirectional replication: non-CDB to PDB
    1. After replication catchup, Failover to PDB
- DBMS_PDB package (see above)


## Managing CDBs and PDBs
### Establish connection to a CDB/PDB 

- SQL*Plus connect
    - connect to root DB or a PDB
    - Get Current Container: SYS_CONTEXT('USRENV', 'CON_NAME')
    - Get Current Container: `SHOW CON_NAME`, `SHOW CON_ID`
        - Function CON_NAME_TO_ID(), CON_DBID_TO_ID()
    - Set Current Container: ALTER SESSION SET CONTAINER=
    - Only common user has CDB$ROOT as current container
        - To use SQL with "CONTAINER=ALL", user must connected to CDB$ROOT
    - Both common user and local user has PDB as current container
- Database Service
    - Default service name same as PDB name
    - tnsnames.ora or Oracle Service Name
    - CDS_SERVICES: name, network_name, pdb
    - Service not dropped at unplug or drop of PDB
- Admin Roles: CDB_DBA and PDB_DBA
    - DBA Task common in CDB and PDB:
        - Manage TS, datafile, tempfile
        - Manage schema objects
    - DBA Task only in CDB:
        - Start/Stop CDB
        - Modify or run DDL on CDB or root db
        - Manage: process, memory, alerts, control files, undo, redo logs
        - Create/Drop, Plug/Unplug PDB
- Container clause in DDL
    - "CONTAINER=pdb" to create local user specific to PDB
    - "CONTAINER=ALL" to create common user
    - Common User must have prefix "C##"
- Connect to CDB
    - Privilege: CREATE SESSION at root db grant to common user
    - OS authenication (to CDB) as sysdba  `sqlplus / as sysdba`
    - Local connection (system user of CDB)  `conect system/<password>`
    - Net Services Name  `connect c##dba@cdb1`
- Connect to PDB
    - Privilege: CREATE SESSION at specific dba
        - locally granted to local user
        - locally granted to common user
        - commonly granted to common user 
    - Net Services Name `connect sys/<password>@pdb1 as sysdba`
        - tnsnames: SERVICE_NAME
        - Create service by SRVCTL: `srvctl add service -db cdb1 -service pdb1_svc -pdb pdb1`
        - If not managed by Oracle Clusterware: DBMS_SERVICES package
    - Switch container
        - Reconnect: `connect local_user@pdb1`
        - Alter Session: `ALTER SESSION SET CONTAINER` : Only for common user
            - Need Privilege for specific PDB or commonly: SET CONTAINER

### Start up and shut down a CDB/PDB 

- Startup
    - STARTUP
    - STARTUP NOMOUNT and then ALTER ... MOUNT/ OPEN
- CDB Open Mode
    - NOMOUNT: memory assigned: No PDB visible
    - MOUNT: controlfile secured: Datafile and PDBs mounted
    - OPEN: root db datafiles and redo log opened
        - Seed DB in READ ONLY status at CDB open
        - PDBs not automatically opened unless there is trigger
- Trigger to start PDBs
    - `create tigger open_pdbs after startup on database begin execute immediate 'alter pluggable database all open;' end open_pdbs`
- CDB Shutdown
    - `shutdown` as non-CDB with following sequence:
    1. Shutdown all closed
    1. CDB closed (handle controlfile)
    1. CDB dismounted (only have memory and process)
    1. Instance shutdown
- PDB Open Modes
    - MOUNTED: All change to datafile. No view/change to data
    - OPEN READ ONLY: View data only
    - OPEN READ WRITE: Normal and operational
    - OPEN MIGRATE: Upgrade and catalog scripts only
- Open PDBs by common user connected to root db
    - `ALTER PLUGGABLE DATABASE pdb1, pdb3 open`
    - `ALTER PLUGGABLE DATABASE all except pdb2 open restricted`
    - `STARTUP PLUGGABLE DATABASE pdb1 force`
    - Cannot startup **all** PDB. Only Alter all pdb.
    - **Connected to PDB**: may drop keyword PLUGGABLE
- Close PDBs by common user connected to root db
    - `ALTER PLUGGABLE DATABASE pdb1, pdb3 close immediate`
    - `ALTER PLUGGABLE DATABASE all except pdb2 close`
    - **Connected to PDB**: may drop keyword PLUGGABLE
    - Make sure you are connected to PDB: `ALTER DATABASE` will close **whole** CDB

### Change instance parameters for a CDB/PDB 

- Parameters at PDB:
    - Only one SPFILE per CDB
    - V$PARAMETER: ISPDB_MODIFIABLE ('TRUE'/'FALSE')
        - Memory parameters and non-pdb-modifiable parameters are not modifiable at At PDB.
    - V$SYSTEM_PARAMETER: Parameter by CON_ID (container ID)
    - `show parameter`
    - `alter system set <parameter>=<value>`
    - At PDB no need to specify scope
        - Keep in memory at close of PDB
        - Store in disk at close of CDB
- ALTER PLUGGABLE DATABASE
    - Can use `ALTER DATABASE` when connected to PDB
    - But cannot specify _pdb_state_clause_
- Statistics
    - Only common user connected to root db can view optimizer statistics for root and PDBs
    - PDB user can view optimizer statistics for that PDB
    - Must run Database Replay in root db by common user
    - Must run ADDM in root db by common user
        - In RAC, ADDM can be run at instance or at whole database
    - Must run SQL Tuning Advsior or SQL Performance Analyzer (SPA) by common user
        - Need SET CONTAINER privilege to gather AWR data for specific PDB
- Manage Objects
    - Common user can own objects in root db as well as PDBs
    - Oracle recommends common users only have triggers and objects used in their definition (!)
- Data dictionary
    - Standard Views: V$_XXX, GV$_XXX and [DBA|ALL|USER]_XXX
    - Common user can view data-dict for root db or PDB
    - User connected to PDB can view data-dict for that PDB
    - _Container data objects_ = table or view has data pertaining multiple containers
    - PDB has a metadata link to root's metadata
    - CDB_XXX: All objects in CDB across all PDBs
        - Column _CONTAINER_DATA_ (!) decide which PDB related to CDB_XXX views
        - Column _CON_ID_
            - 0: Apply to all containers in CDB
            - 1: Apply to root db
            - 2: Apply to seed db
            - 3 to 254: Other PDBs
    - DBA_XXX: All objects in connected PDB
    - CDB_PDBs: All PDBs in CDB
    - CDB_PDB_HISTORY: History for each PDB. Column OPERATION: Plug/Unplug
    - CDB_PROPERTIES: Properties of each container
    - CDB_CONTAINER_DATA: (!) CONTAINER_DATA
    - CDB_SERVICES: Database services for Network connection
    - CDB_OBJECTS: All container objects. Column SHARING= type of link
    - CDB_VIEWS: All views. Column CONTAINER_DATA= whether is container object
    - CDB_tablespaces: All tablespaces in CDB
    - CDB_data_files: All data files in CDB
    - CDB_users: All users in CDB. Column COMMON= common user or not
    - CDB_roles: All roles in CDB. Column COMMON= common role or not
    - [G$|V$]DATABASE: Database Information
    - [G$|V$]CONTAINERS: Container Information
    - [G$|V$]PDBS: all PDB associated to current PDB
    - [G$|V$]SYSTEM_PARAMETERS: Init Parameters for different PDBs
    - RC$_PDBS: Recovery Catalog about PDB backups
    - When connected to PDB: data of CDB_XXX is DBA_XXX
- Enable common user to data on PDB
    - `ALTER USER c##kk_admin SET CONTAINER_DATA= (cdb$root, pdb2, pdb3) FOR V$SESSION CONTAINER=CURRENT`
    - cdb$root is required for common users

## Managing Tablespaces, Common and Local Users, Privileges and Roles
### Manage tablespaces in a CDB/PDB 

- SQL
    - `CREATE TABLESPACE` same as non-CDB. It is created at connected container.
    - `ALTER PLUGGABLE DATABASE default tablespace ts1`;
        - `ALTER DATABASE` can be used when connected to PDB for compatibility
    - CDB has only **one** default temp TS or tmp TS group
        - But other temp TS can be assigned to users, particularly local users

### Manage users and privileges for CDB/PDB 

- Local User/ Role are restricted to a PDB.
- Common User can:
    - grant privileges to common role or common user
    - ALTER DATABASE with recovery clause apply to whole CDB
- User Management
    - Syntax: `create user user01 identified by xyz container=current`
    - Create local user
        - DEFAULT container is CURRENT (connected container)
        - may set CONTAINER to specific PDB
        - No local user for root db
        - Name of local user must not have prefix `c##` or `C##`
    - Create common user
        - Common user is created for all containers
        - Require Privileges: CREATE USER and SET CONTAINER
        - Must connect to root container
        - Set `CONTAINER=ALL`
            - So local user cannot create common user
        - Name of common user must have prefix `c##` or `C##`
- Role Management
    - Syntax: `create role role01 container=current`
    - Create local role
        - DEFAULT container is CURRENT (connected container)
        - may set CONTAINER to specific PDB
        - No local role for root db
        - Name of local role must not have prefix `c##` or `C##`
    - Create common role
        - Common role is created for all containers
        - Require Privileges: CREATE ROLE and SET CONTAINER
        - Must connect to root container
        - Set `CONTAINER=ALL`
            - So local user cannot create common role
        - Name of common user must have prefix `c##` or `C##`
            - Oracle-supplied role exempted this naming rule
    - Syntax: `GRANT c##role to c##user CONTAINER=ALL`
    - Grant Role:
        - Need Privilege `GRANT ANY ROLE` or Grant Role under `WITH ADMIN OPTION`
        - No grant restriction: Can grant local/common role to local/common user/role
            - But local user only has privileges on its container regardless of granted roles
    - Revoke Role:
        - revoke a common role commonly by `CONTAINER=ALL`
        - revoke a local role locally by `CONTAINER=pdb`
        - Cannot locally revoke a common role
    - Oracle-Supplied Roles:
        - CBA_DBA: common DBA role
        - PDB_DBA: local DBA role with no Privilege
        - DBA: backward compatibility
- Privilege Management
    - Privilege is neither local nor common by itself
    - Privilege is local or common: when it is _granted_ locally or commonly.
    - Common users can be granted some privilege commonly and some locally
    - Only Common user can grant privilege commonly, only to common user
        - privilege granted commonly applicable to all PDBs
        - System or object privilege can be granted commonly
    - Syntax: `GRANT drop user TO c##bar CONTAINER=ALL`
    - Grant a privilege locally by `CONTAINER=CURRENT`
    - Revoke common privilege needs to specify `CONTAINER=ALL` and connect to root db
    - Revoke local privilege needs to specify `CONTAINER=pdb1` or connect to that PDB

## Auditing
### Enable and configure Unified Audit Data Trail

- Issue: Security Threats and Compliance
- Aim: Consolidated approach on audit trail - Unified Audit
- Unified Audit include records from:
    - Normal Audit records and SYS audit records
    - Fine Grained Audit by package `DBMS_FGA`
    - Real Application Security
    - Recovery Manager
    - Database Vault
    - Label Security
        - Data Mining
        - Data Pump
    - SQL*Loader
- Benefit and Features:
    - All audit trail recorded owned by user `AUDSYS`
        - By default in SYSAUX TS
        - Oracle recommend to have dedicated TS for Unified Audit
            - `DBMS_AUDIT_MGNT.SET_AUDIT_TRAIL_LOCATION`
        - User `AUDSYS` locked by default
    - Audit trail data are readonly. SYS user activity can audited
    - Audit options can be grouped in Audit policy
        - Can exempt some user or configure condition on audit
    - Performance improved: SGA to keep audit record and flush
- Multitenant
    - Audit setting can be applied to whole CDB or only specific PDB
        - Audit policy enabled only for root container is also local
    - But FGA can be applied only to CDB
- Require: Always available. No License or Init Parameter needed
    - Check Usage: `select value from v$option where parameter= 'Unified Auditing'`
    - Default: Mixed mode auditing
        - Support traditional audit
            - Oracle default policy
                - `ORA_SECURECONFIG`： 11g secure configuration audit options
                - `ORA_ACCOUNT_MGMT`: User, Role, Grant, Revoke
                - `ORA_DATABASE_PARAMETER`: alter database, alter system, create spfile
            - Default Audited Actions:
                - Connects as SYSDBA, SYSOPER, SYSBACKUP, SYSASM, SYSKM, SYSDBA
                - Startup, Shutdown, ALTER SYSTEM
        - Support Unified Audit also
        - May switch to Exclsuive Unified Audit
            - Switching require relinkning of Oracle executable (require shutdown and startup)
                - `cd $ORACLE_HOME/rdbms/lib`
                - Turn on: `make -f ins_rdbms.mk uniaud_on ioracle ORACLE_HOME=$ORACLE_HOME`
                - Turn off: `make -f ins_rdbms.mk uniaud_off ioracle ORACLE_HOME=$ORACLE_HOME`
- Audit Flushing
    - Handled by process GEN0
    - One queue is held at SGA
        - May **lose data at instance crash**
    - Second queue flushed to disk
        - Force flush: `DBMS_AUDIT_MGNT.FLUSH_UNIFIED_AUDIT_TRAIL`
        - _Queued-write mode_ by default: 1MB buffer in SGA
            - Buffer size can be change by init parameter UNIFIED_AUDIT_SGA_QUEUE_SIZE
            - Max 30MB: Enlarge it consume memory in SGA
        - Can change to immmediate-write mode
            - `DBMS_AUDIT_MGNT.SET_AUDIT_TRAIL_PROPERTY(DBMS_AUDIT_MGNT.AUDIT_TRAIL_UNITED, DBMS_AUDIT_MGNT.AUDIT_TRAIL_WRITE_MODE, DBMS_AUDIT_MGNT.AUDIT_TRAIL_IMMEDIATE_WRITE)`
            - Change back by argument `DBMS_AUDIT_MGNT.AUDIT_TRAIL_QUEUED_WRITE`
    - View at `SYS.UNIFIED_AUDIT_TRAIL`, based on table owned by `AUDSYS`
        - Viewable by role `ADUIT_ADMIN` and `ADUIT_VIEWER`
        - Old view: `SYS.AUD$`
- Extended Aduit Information (EAI)
    - Old way: Basic Audit Information (BAI)
    - New column:
        - FGA: FGA_POLICY_NAME
        - Data Pump: DP_TEXT_PARAMETER1, DP_BOOLEAN_PARAMETER1
        - RMAN: RMAN_OPERATION value= 'BACKUP', 'RESTORE', 'RECOVER'
            - RMAN operations always audited
        - Database Vault: DV_XXX
- Enable EAI for Data Eump (example)
    1. Create audit policy for component
        - `create audit policy db_p1 _actions_ component=datapump ALL`
    1. Enable audit policy
        - `audit policy db_p1`
    1. Perform some data pump
    1. Flush audit trail to disk `DBMS_AUDIT_MGNT.FLUSH_UNIFIED_AUDIT_TRAIL`
    1. View audit record at `SYS.UNIFIED_AUDIT_TRAIL`

### Create and enable audit policies 

- Role:
    - `ADUIT_VIEWER`: View audit data
    - `AUDIT_ADMIN`： Create/Drop, Enable/Disable Policy/ FGA policy; View and Manage audit data
- Audit common object requires common policy; Audit local object requires local policy
- Common policy: available to all PDBs
    - Create at root container (so created by common user)
    - Enable for common users only
    - Policy creater must be AUDIT_ADMIN role
    - Audit only common objects
- Local policy: available to single PDBs or limited to root container
    - Create at root container or at PDB
    - Create at root container: Only audit objects. Cannot audit privilege or role
    - Create at PDB: enable for PDB only. Only local object/privilege/role/etc
    - Need AUDIT_ADMIN role grant for container (or ALL)
- Create Policy Scope:
    - Audit Action:
        - User accounnt, Role, Privilege
        - Action on objects, include trigger, function, procedure, package
        - Application Context value
        - Component Activity: RMAN, Data Pump, etc
- Create Policy Syntax:
    - `CREATE AUDIT POLICY policy01 _action1_ [,_action2_] [CONTAINER= CURRENT | ALL]`
    - `DROP AUDIT POLICY policy01`
        - (!) Cannot drop an enabled policy. Disable it first.
        - Must connect to root container to drop common policy
- Create policy Long Syntax:
    - Full: https://docs.oracle.com/en/database/oracle/oracle-database/12.2/sqlrf/CREATE-AUDIT-POLICY-Unified-Auditing.html
    - Targets of Audit (one or more):
        - privilege_audit_clause: List of system privilege(s)
        - action_audit_clause: List of standard action(s) or component(s)
        - role_audit_clause: List of role(s)
        - System Example: `CREATE AUDIT POLICY p02 PRIVILEGES drop any table ACTIONS drop table ROLE dba`
        - Object Example: `CREATE AUDIT POLICY p03 ACTIONS select, insert ON hr.employees`
    - Condition clause: Specify condition and when to evaluate condition
        - Evaluate: per statement, per session or per instance
        - Condition: SYS_CONTEXT
        - Example: `CREATE AUDIT POLICY p04 ACTIONS alter ON oe.orders WHEN 'SYS_CONTENT(''USERENV'',''SESSION_USER'')=''TOM'''`
    - container clause: CONTAINER value
- Enable and Disable Policy:
    - Enable Policy `AUDIT POLICY`
        - AUDIT POLICY p02 [by user_list] [except user_list] [whenever (NOT) successful]
    - Disable `NOAUDIT POLICY <name>`
- Alter Policy `ALTER POLICY`:
    - Add target `ALTER POLICY p02 ADD ROLE c##role1`
    - Drop condition `ALTER POLICY p04 CONDITION DROP`
    - Altered policy do not need re-enable unless
        - auditing activiated of user session
        - auditing system audit option (!)
- Aduit Application Context  `AUDIT CONTEXT`
    - Syntax: `AUDIT CONTEXT NAMESPACE namespace CONTEXT attribute(s) BY user(s)`
    - Syntax: `NOAUDIT CONTEXT NAMESPACE namespace CONTEXT attribute(s) BY user(s)`
- DataDic:
    - `AUDIT_UNIFIED_POLICY`: All created policies
        - Column CONDITION_EVAL_OPT: Condition text
    - `AUDIT_UNIFIED_ENABLED_POLICY`: All enabled policies
    - `AUDIT_UNIFIED_CONTEXT`: All audited context (no enable/disable state)

## Privileges
### Use administrative privileges 

- Issue: Proliferation of privileges and assignment of unneeded privileges
- SYSDBA is kept for backward compatibility only
- System privilege SYSBACKUP, SYSDG and SYSKM define in favor of SYSDBA
    - OS groups
        - OS groups created for these system privileges
            - When DB created by DBCA or OUI, DBA will be given choice to create OS groups
                - Default OS group: OSBACKUP, OSDG, OSKM
            - OS groups stored at $ORACLE_HOME/rdbms/lib/config.[cs] file
                - relink need for change of OS group
            - OS authenication requires OS user belongs to respective group
                - Otherwise: network, password or diectory based connection
        - SQL*PLUS: `connect / as sysbackup` and `show user`
        - RMAN: `rman target "/ as sysbackup"` and `select user from dual`
        - Oracle recommend to grant SYSBACKUP to DBA or backup user
            - To audit/ identify the user (not privilege) doing backup operations
    - Must create Password file so that user can connect with these system privileges
        - `orapwd file=fn entries=nbr force=yn asm=yn dbuniquename=dbname format= sysbackup=yn sysdg=yn syskm=yn delete=yn input_file=`
            - format= "LEGACY" or "12". Only "12" support entries for sysbackup, sysdg, syskm
                - all format support sysdba and sysadm (manage ASM instance)
            - input_file: You can copy a legacy password file and create a new password file with new entries
            - sysbackup, sysdg, syskm: whether to create entry for system privilege in password file
        - Init Parameter REMOTE_LOGIN_PASSWORDFILE=exclusive
        - View: V$PWFILE
    - New system privileges are audited same as SYSDBA and SYSOPER, for both unified audit or standard audit
- SYSBACKUP : backup, restore and recover
    - Create or Drop database
    - Create control file
    - Create PFILE/ SPFILE
    - Startup/ Shutdown database
    - Manage restore point
    - Flashback database
    - Change archivelog mode
    - At PDB, may grant SYSBACKUP to a local user for backup at PDB only
- SYSDG : Data Guard admin tasks; Data Guard Broker and DGMGRL (CLI)
    - Startup/ Shutdown database
    - Manage restore point
    - Flashback database
    - Run DGMGRL
    - Start observer (!)
    - Enable application to request immmediate invocation for fast-start Failover
- SYSKM : TDE Keystore operations
    - Create/ Open/ Close Keystores
    - Create/ change master key for encryption
    - Manage encryption keys for column or tablespace encryption

### Create, enable and use privilege analysis 、

- Aim: Track Privileges used/ not used during a database session
- Require: (None)
    - Database Vault not required; despite this feature mentioned in Database Vault documentation
- Overall workflow
    1. Create Privileges analysis policy; Set type and conditions
    1. Enable Privileges analysis policy: Start of database session being tracked
    1. Disable Privileges analysis policy: End of database session being tracked
    1. Generate report on used/ not used privilege over tracked session
    1. Drop Privileges analysis policy or Generate Report
    - Package: `DBMS_PRIVILEGE_CAPTURE`
- Type of Privileges analysis policy
    - Database analysis: across entire database and Unconditional
        - Type value: `DBA_PRIV_CAPTURES.g_database`
    - Role analysis: analyze privileges through list of granted roles
        - Type value: `DBA_PRIV_CAPTURES.g_role`
        - Cannot analysis Privileges granted through SYS
        - Role PUBLIC is good candidate to be analyzed
    - Context-specific analysis: 
        - Type value: `DBA_PRIV_CAPTURES.g_context`
    - Role and Context-specific analysis: combined of role and condition
        - Type value: `DBA_PRIV_CAPTURES.g_role_and_context`
    - At most _one database_ and at most _one non-database_ privileges analysis policy **can be enabled** at any time
- Create Privileges analysis policy `CREATE_CAPTURE()` procedure
    - Arguments: name, description, type, role, condition
    - `exec DBA_PRIV_CAPTURES.CREATE_CAPTURE(name=>'pp1', description=>'all', type=>DBA_PRIV_CAPTURES.g_database)`
    - Specify role by `role=> role_name_list('pdb1_dba', 'pdb2_dba')`
        - The function `role_name_list()` allows up to 10 roles
    - Specify condition as text which can be evaluated to boolean
        - Only allow SYS_CONTEXT(), relational operators (==, >=, <=, >, <, <>, BETWEEN, IN) and logic operators (AND, OR, NOT)
        - Example: `'condition=> SYS_CONTEXT(''USER_SESSION'', ''SESSION_USER'') IN (''HR'', ''OE'')'`
    - Specify both role and condition at type `DBA_PRIV_CAPTURES.g_role_and_context`
- Other procedure of the package 
    - Enable:  `exec DBA_PRIV_CAPTURES.ENABLE_CAPTURE(name=> 'pp1')`
        - Enabled policy keep enabled until stop of database
    - Disable: `exec DBA_PRIV_CAPTURES.DISABLE_CAPTURE(name=> 'pp1')`
    - Report:  `exec DBA_PRIV_CAPTURES.GENERATE_RESULT(name=> 'pp1')`
    - Drop:    `exec DBA_PRIV_CAPTURES.DROP_CAPTURE(name=> 'pp1')`
        - Report data are cleared at drop of policy
- Views
    - View of created policies: `DBA_PRIV_CAPTURES`
    - View of generated report: `DBA_USED_SYSPRIVS`, `DBA_USED_OBJPRIVS`, `DBA_USED_PRIVS`, `DBA_UNUSED_PRIVS`
    - View of usage path of used privilege
        - Column PATH on `DBA_USED_SYSPRIVS_PATH` and `DBA_USED_OBJPRIVS_PATH`

- AUTHID (Invoker rights vs definer rights)
    - Recap of 11g
        - AUTHID=DEFINER (default): PL/SQL executed under definer's rights
        - AUTHID=CURRENT_USER: PL/SQL executed under invoker's rights
    - 12c new feature
        - When a user execute PL/SQL with invoker's right, check whether
            - owner has (object privilege) INHERIT PRIVILEGE on invoker 
            - owner has (system privilege) INHERIT ANY PRIVILEGE
            - Issue an error at execution if owner has no both privileges
            - Grant: `GRANT INHERIT PRIVILEGE ON USER HR to usr1`
        - View Qualifer `BEQUEATH CURRENT_USER`
            - By default views are qualified with `BEQUEATH DEFINER`
            - Viewer gather data by definer's privileges on SQL of view
            - When qualified with `BEQUEATH CURRENT_USER`, Viewer gather data by viewer's privileges on SQL of view
                - Check INHERIT PRIVILEGE or INHERIT ANY PRIVILEGE similar to PL/SQL
                - Issue an error at viewing if owner has no both privileges

## Oracle Data Redaction
### Use and manage Oracle Data Redaction policies 

- Aim and Issue
    - Issue: Protecting security related application being viewed or misused
    - Aim: Redact (mask) sensitive data
    - Aim: Modify data on the fly when queried without changing data on disk
    - Aim: No measurable performance degradation and usable in production system
        - Exception: Consume resource to evaluate DBA-defined regex within redaction
    - Exempted: SYS, SYSTEM users, and RMAN backup/restore, Data Pump, Data Replication, Patching/Upgrade activity
        - System Privilege: EXEMPT REDACTION POLICY
        - For example: EXP_FULL_DATABASE_ROLE and DBA has this privilege
    - Effect: Redaction resolved at last moment before query returns results to caller
    - Oracle recommend to define redact policies by white lists
- View chain of Redaction 
    - When an redaction is enabled on a table, it propagates to view and mview refer to that table
    - Also propagate to view/mview on view/mview _recursively_
    - Redaction resolved only at _query_. No effect to mview data rebuild
- Query redaction sequence:
    - Nested functions are redacted innermost
        - Data is redacted when affected value is evaluated
    - Inline views are redacted outermost
    - Where clause never redacted
- Redaction restriction: Cannot redact
    - Objects owned by SYS or SYSTEM
    - Columns of specific data types (outside character, number, date)
    - Virtual Columns
    - At most one policy may be defined for any table or view
- Package `DBMS_REDACT` https://docs.oracle.com/database/121/ARPLS/d_redact.htm
- Redaction Policy
    - What to redact: Schema `object_schema`, Object `object_name`, Column `column_name`
        - Only one column allowed at initial definition of redaction policy `ADD_POLICY()`
        - More columns may be added or dropped at alteration of redaction policy `ALTER_POLICY()`
    - Condition to redact `expression`: Boolean expression by SYS_CONTEXT() and relational operators
- Add function policy `ADD_POLICY()`
    - Policy name and description `policy_name`, `policy_description`
    - Condition to redact `expression`: Use `1=1` for always true
    - Enable/Disable `enable`: Default is true
    - Function type `function_type` (see below)
    - Specific arguments depends on function types
        - Function Parameter `function_parameters` (!)
        - Regex arguments `regexp_*`
- Function types `function_type` of redaction: None, Full, Partial, Random, Regular Expression (regex)
    - None `DBMS_REDACT.NONE`: As an redaction policy but do nothing
    - Full data redaction `DBMS_REDACT.FULL`
        - Character: Single blank space
        - Number: Zero
        - Date: date'2001-01-01'
        - Can be changed by `DBMS_REDACT.UPDATE_FULL_REDACTION_VALUES()` procedure: apply to all policies
    - Random data redaction `DBMS_REDACT.RANDOM` specification (!)
        - Character: Random character of specified length
        - Number: Random number of specified precision
        - Date: Random date
    - Partial data redaction `DBMS_REDACT.PARTIAL` specification
        - Important argument: `function_parameters`
        - Character: Offset position (start position), Nbr of character to redact, Redaction character
        - Number: MASKFROM (start position), MASKTO (end position), Redaction character
        - Date: Attribute masked (year, month, date, hour, minute, second)
    - Regex data redaction `DBMS_REDACT.REGEXP` specification
        - Search regex pattern: argument `regexp_pattern`
        - Replace String: argument `regexp_replace_string`
        - Starting position: argument `regexp_position`
            - 1 (`RE_BEGINNING`) for beginning
        - Ocurrance of replacement: `regexp_ocurrance`
            - 0 (`RE_ALL`) for always replace; 1 for replace only once; Nbr for countable occurance
        - regex behaviour indicator (e.g. case sensitive or not): `regexp_match_parameter`
- Alter policy `ALTER_POLICY()`
    - Alter Action: argument `action`
        - Only one action can be choose at which invoke of ALTER_POLICY()
        - Add column: `ADD_COLUMN`
        - Drop column: `DROP_COLUMN`
        - Alter policy expression: `MODIFY_EXPRESSION`
        - Change **function type, function parameter or regex parameter**: `MODIFY_COLUMN`
- Enable/ Disable Policy
    - `DBMS_REDACT.ENABLE_POLICY(object_schema=>'hr', object_name=>'cust_info', policy_name=>'rp01')`
    - `DBMS_REDACT.DISABLE_POLICY(object_schema=>'hr', object_name=>'cust_info', policy_name=>'rp01')`
- Views: `REDACTION_POLICIES` and `REDACTION_COLUMNS`
    - Enabled and Expression belongs to redaction policy
    - Function type, function parameter and regex parameter belongs to redacted column, not to policy

## SQL Tuning
### Use Adaptive Execution Plans 

- Issue: Insufficient statistics to pick best execution plan
- Require:
    - Init Para OPTIMIZER_FEATURES_ENABLE=12.1.0.1 or later
    - Init Para OPTIMIZER_ADAPTIVE_REPORT_ONLY=FALSE (default)
        - _reporting-only mode_ when true 
        - Adaptive Execution Plans are reported but never used
- Concept: https://oracle-base.com/articles/12c/dynamic-statistics-12cr1
- Concept: https://www.oracle.com/technetwork/database/bi-datawarehousing/twp-optimizer-with-oracledb-12c-1963236.pdf
- Adaptive Plan
    - Default Plan: Optimizer plan based on existing statistics
    - Subplan: Alternative plan that optimizer may choose
    - Final Plan: Optimizer plan based on adaptive statistics
    - Defer decision to prepare adaptive statistics and adopt final plan
    - Adopted final plan used for subsequent executions
        - Column `IS_RESOLVED_DYNAMIC_PLAN` at `V$SQL` (YN)
- Adaptive Statistics (See below)
    - Dynamic statistics (particularly on cardinality)
    - Automatic reoptimization
    - SQL Plan directives
- Alternative join at Subplan
    - Nested loop join vs Hash join
        - Nested loop join used for low cardinality at adaptive statistics
        - Hash join used for high cardinality at adaptive statistics
        - Threshold set by Optimizer
    - Broadcast Distribution vs Hash Distribution at Parallel query
        - Hybrid data Distribution (!): Method of Distribution can be switched 
        - Broadcast Distribution used for low cardinality at adaptive statistics
        - Hash Distribution used for high cardinality at adaptive statistics
        - Threshold= 2 x degree of parallelism allowed for that query
        - https://oracle-randolf.blogspot.com/2015/02/12c-parallel-execution-new-features.html
    - Bitmap Pruning (!)
- Check whether Adaptive Plan used
    - Explain Plan shows whether a plan is adaptive plan or default plan
    - DBMS_XPLAN.DISPLAY_CURSOR shows final plan

- Dynamic statistics
    - Require: `OPTIMIZER_DYNAMIC_SAMPLING`= 11 
        - value 2 is backward compatible to 11g
    - Was _dynamic sampling_ in 11g
        - against cases of missing statistics
        - default level= 2
        - default sample size= 64 blocks
        - held in memory not persist
    - Dynamic statistics
        - Optimizer decides to gather dynamic statistics on:
            - Missing statistics: New object or never gathered statistics
            - Stale statistics: 10% or more rows modified after statistics gathering
            - Insuffient statistics: When optimizer mis-estimate selectivity
                - At Query with filter, join or group by
                - maybe because of missing histogram to identify data shew, or missing extended statistics
        - augument existing statistics
        - Dynamic statistics persist
        - Support joins, group by and non-parallel query
    - In environment that require queries be compiled fast
        - Example: primarily unrepeated OLTP SQL
        - Best practice: disable dynamic statistics by OPTIMIZER_DYNAMIC_SAMPLING= 0
- Automatic reoptimization
    - Issue: Adaptive plan cannot modify _join order_ in the middle of execution
    - Aim: Reoptimization has broader scope than Dynamic statistics
        - Optimizer change plan to subsequent execution but not current execution
        - Statistics and Performance are gathered and feedback to statistics and SQL prasing
        - Explain plan will tell whether statistics feedback used
        - View `V$SQL` column IS_REOPTIMIZABLE (!)
    - Statistics feedback (also cardinality feedback)
        1. Enable monitoring statistics feedback for:
            - Missing statistics, or
            - Complex filter predicate, or
            - Complex operators: cannot accurately compute cardinality estimates
        1. Compare cardinality estimate with nbr of rows returned. Store correct cardinality if they vary widely
        1. Create a SQL Plan directive so that other SQL can take advantage of new cardinality
        1. Turn off monitoring statistics feedback regardless whether correction take place
        1. Use improved cardinality statistics in subsequent executions
    - Performance feedback
        - Init Para `PARALLEL_DEGREE_POLICY`
            - MANUAL: default; disable automatic degree of parallelism, statement queuing and in-memory parallel execution
            - LIMITED: disable statement queuing and in-memory parallel execution
                - Enable automatic degree of parallelism on accessing table/view with DEFAULT parallelism clause
            - AUTO: enable automatic degree of parallelism, statement queuing and in-memory parallel execution.
            - ADAPTIVE: Same as AUTO with Performance feedback
            - Hint _PARALLEL_ override `PARALLEL_DEGREE_POLICY`
        - Feedback continue to affect subsequent executions even when `PARALLEL_DEGREE_POLICY` is no longer ADAPTIVE (!)
        1. Optimzier select degree of parallelism and enable performance monitoring
        1. Compare parallelism selected and degree of parallelism based on execution statistics
        1. If they vary widely, store collected statistics as feedback and mark statement for reparsing
        1. Subsequent executions use new degree of parallelism and performance statistics
    
- SQL Plan directives
    - Periodically gather missing data to help optimzing SQL Plans
        - Initially stored in shared pool
        - Store in SYSAUX every 15 min; View: `DBA_SQL_PLAN_DIRECTIVES` and `DBA_SQL_PLAN_DIR_OBJECTS`
        - Purged if not used for one year
        - Created upon SQL expression, not SQL ID
            - It affect _similar_ SQL, while previous tools only affect same SQL
        - SQL driective may suggest dynamic sampling to improve plan on wrong cardinality estimates (!)
    - Hint GATHER_PLAN_STATISTICS to force gathering statistics and possible feedback
    - Package `DBMS_SPD`
        - Flush Directive: `exec DBMS_SPD.FLUSH_SQL_PLAN_DIRECTIVE`
        - Drop Directive: `exec DBMS_SPD.DROP_SQL_PLAN_DIRECTIVE(directive_id => nbr)`


### Use enhanced features of statistics gathering 

- Enhancements on statistics gathering
    - Online stats gathering at bulk-load
    - Concurrent collection of stats
    - New and more efficient histogram
    - Extended stats based on actual workload
- Online stats gathering at bulk-load
    - Issue: Take too much to gather stats manuallyafter CTAS or IAS
    - Aim: Stats are gathered online (non-blocking) after CTAS or IAS
    - Parallel insert are direct path insert by default
    - View `DBA_TAB_COL_STATISTICS` column NOTES: value STATS_ON_LOAD when it is gathering online
    - Does not gather index stats and histograms
        - Invoke `DBMS_STATS.GATHER_TABLE_STATS(...)` to fill missing gap
    - Not gathered for
        - Oracle owned schema
        - Nested table
        - IOT
        - External table
        - Table with virtual column
        - Global Tempoarily Table defined as ON COMMIT DELETE ROWS
        - PUBLISH preference set to true (!)
        - Partitioned, incremental=true, and extended syntax not used (!)
- Concurrent collection of stats
    - Requires
        - Init Para: JOB_QUEUE_PROCESSES >=4 limit conncurrency over all jobs
        - Database Resource Manager (DRM) has an enabled plan
        - Advanced Queue (AQ)
        - Oracle Scheduler (if stats gathered by schedulers)
    - Each table can have its own gather stats job (on allowed JOB_QUEUE_PROCESSES)
        - DBMS_STATS package may gather stats of several small partitions/tables by one thread not concurrently
    - DRM: May use default or customized plan to limit ORA$AUTOTASK consumer group
    - Preference `CONCURRENT` of `DBMS_STATS.SET_GLOBAL_PREFS()`:
        - MANUAL: Concurrency only for manual stats gathering
        - AUTOMATIC: Concurrency only for automatic stats gathering
        - ALL: Concurrency only for both manual and automatic stats gathering
        - OFF: No Concurrency; Default
    - Steps to enable Concurrent stats collection
        1. ALTER SYSTEM SET JOB_QUEUE_PROCESSES= 8
        1. ALTER SYSTEM SET RESOURCE_MANAGER_PLAN= 'DEFAULT_PLAN'
        1. exec DBMS_STATS.SET_GLOBAL_PREFS('CONNCURENT', 'ALL')
        1. exec DBMS_STATS.GATHER_SCHEMA_STATS('SH')
        1. View DBA_OPTSTAT_OPERATION_TASKS for progress
        1. exec DBMS_STATS.SET_GLOBAL_PREFS('CONNCURENT', 'OFF')  [optional]
    - DBA may set temporarily DRM plan to promote parallelism of stats collection
- New and more efficient histogram
    - View: USER_TAB_HISTOGRAMS
    - Old way:
        - Frequency histogram and height balanced histogram on column cardinality and shewness
        - Create frequency histogram when cardinality < user specific histogram bucket (nb) (new: Frequency and Top Frequency) (!)
        - When sampling percent set to AUTO, histogram to be created is "Height balanced" (new: Hybrid)
    - Top Frequency histogram, Create when
        - Sampling percent= AUTO
        - Cardinality >= nb (default 254)
        - Cardinality > 254
        - Top nb values has more than p% rows; p%= (1-(1/nb)) x 100%
        - Top Frequency histogram focus on popular values: small number of value has large portion of rows
    - Hybrid histogram
        - Combined from Frequency histogram and Height balanced histogram (!)
        - Create when
            - Sampling percent= AUTO
            - Not qualifed for Top Frequency histogram
            - Cardinality >= nb (default 254)
- Extended stats based on actual workload
    - Statistics focus on cardinality
        - Column group stats: multiple columns at WHERE clause
        - Expression stats: expression of column at WHERE clause
    1. Enable Workload Monitoring
        - `exec DBMS_STATS.SEED_COL_USAGE(null, null, 600)`
    1. Running Workload: Carry out workload that to be optimized during number of seconds of workload
        - Explain plan (instead of actual workload) also work on prepared list of SQL 
    1. Review Column Group Usage
        - `exec select DBMS_STATS.REPORT_COL_USAGE('SH', 'CUSTOMERS') form dual`
    1. Create Column Group
        - `exec DBMS_STATS.CREATE_EXTENDED_STATS('SH', 'CUSTOMERS')`

### Use Adaptive SQL Plan Management 

- Requires: Oracle Tunning Pack
- Old way of SPM
    - Capture SQL Plans
    - Verify SQL Plans (human)
    - Evolve SQL Plans
- Concepts:
    - SQL Plans baseline: Accepted SQL Plan
        - New SQL Plan are not accepted Plan. Need verification process
        - SQL management base (SMB) stored in SYSAUX
    - `DBMS_XPLAN.DISPLAY_PLAN_BASELINE()` show the stored plan SMB
        - In 11g, this show _compiled execution plan_ of baseline
- SQL Plan Management (SPM) Evolve Advisor
    - (!) Functions misunderstanding `DBMS_SPM`
    - https://docs.oracle.com/database/121/ARPLS/d_spm.htm
    - https://oracle-base.com/articles/12c/adaptive-sql-plan-management-12cr1
    - Require: `OPTIMIZER_CAPTURE_SQL_PLAN_BASELINE`= true
    - New nightly Job: `DBMS_SPM.EVOLVE_SQL_PLAN_BASELINE` and task_name='SYS_AUTO_SPM_EVOLVE_TASK'
        - Can be run manually
        - Accept new plan if it performance better than baseline
        - Poor plan will retire by 30 days
    - SPM components
        - SQL plan baseline capture
        - SQL plan baseline selection
        - SQL plan baseline evolution
    - Functions (!) used to manually evolve plans
        - DBMS_SPM.CREATE_EVOLVE_TASK()
        - DBMS_SPM.EXECUTE_EVOLVE_TASK()
        - DBMS_SPM.REPORT_EVOLVE_TASK()
        - DBMS_SPM.IMPLEMENT_EVOLVE_TASK()

## Resource Manager and Other Performance Enhancements
### Use Resource Manager for a CDB and PDB 

- Multitenant
    - CDB: manage how PDBs compete for resource
        - Cannot define consumer group or share for root container. Only limit PDBs.
    - PDB: manage how consumer groups within PDB compete for resource
- Resource being controlled
    - Share: CPU usage, Nbr of parallel execution
    - Utilitization limits: CPU ultilization limit, Percentage of Parallel execution
        - Limit cannot be exceeded even other PDB do not demand resource
- Pacakge: `DBMS_RESOURCE_MANAGER`
    - https://docs.oracle.com/database/121/ARPLS/d_resmgr.htm (!)
- DRM procedure steps for add/change/drop DRM plan:
    1. Create Pending Area `exec DBMS_RESOURCE_MANAGER.CREATE_PENDING_AREA()`
    1. Create Plan Directive(s): Actual changes to be carried out
    1. Validate Pending Area `exec DBMS_RESOURCE_MANAGER.VALIDATE_PENDING_AREA()`
    1. Submit Pending Area `exec DBMS_RESOURCE_MANAGER.SUBMIT_PENDING_AREA()`
- Manage Plan for CDB
    - Enable/Disable DRM plan
        - `ALTER SYSTEM SET RESOURCE_MANAGER_PLAN= 'daytime_plan'`
        - `ALTER SYSTEM SET RESOURCE_MANAGER_PLAN= ''`
        - Unsetting Init Para `RESOURCE_MANAGER_PLAN` and restart database also disable DRM
    - CDB procedures
        - CREATE_CDB_PLAN
        - CREATE_CDB_PLAN_DIRECTIVE
        - UPDATE_CDB_PLAN
        - UPDATE_CDB_PLAN_DIRECTIVE
        - UPDATE_CDB_DEFAULT_DIRECTIVE
        - DELETE_CDB_PLAN
        - DELETE_CDB_PLAN_DIRECTIVE
    - Plan Directive for PDB are **kept** at unplugged of PDB
    - CDB View: V$RSRC_PLAN, DBA_CDB_RSRC_PLAN, DBA_CDB_RSRC_PLAN_DIRECTIVES
    - Default for CDB resources (updatable by `UPDATE_CDB_DEFAULT_DIRECTIVE` Procedure):
        - share: 1
        - utilitization_limit: 100
        - parallel_server_limit: 100
    - Create Plan for CDB
        - `exec DBMS_RESOURCE_MANAGER.CREATE_CDB_PLAN (plan => 'daytime_plan, comment => 'Some comment')`
    - Create Directive of Plan for pdb1 (NULL means default) and pdb2
```
    exec DBMS_RESOURCE_MANAGER.CREATE_CDB_PLAN_DIRECTIVE ( 
        plan => 'daytime_plan, pluggable_database => 'pdb1', share => 3, utilitization_limit => NULL, parallel_server_limit => NULL 
    )
    exec DBMS_RESOURCE_MANAGER.CREATE_CDB_PLAN_DIRECTIVE ( 
        plan => 'daytime_plan, pluggable_database => 'pdb2', share => 1, utilitization_limit => 70, parallel_server_limit => 70 
    )
```
- Manage Plan for PDB
    - Same as non-CDB except
        - Cannot have multi-level plan in PDB
        - Cannot have subplan in PDB
        - Max 8 consumer groups (32 in non-CDB)
    - Change in arguments
        - share (new, same as CDB)
        - **utilitization_limit** replaces max_utilitization_limit
        - **parallel_server_limit** replaces parallel_target_percentage
    - When there is no plan all sessions are treated equally
- Track Runaway SQL
    - New arguments for `DBMS_RESOURCE_MANAGER.CREATE_PLAN_DIRECTIVE`
        - switch_io_logical: Nbr of I/O to trigger switch consumer group
        - switch_elapsed_time: Time elaspsed in second to trigger switch consumer group
        - (!also see other switch column)
    - Set switch_group=LOG_ONLY: 
        - Do not actually switch group. Only log runaway SQL at V$SQL_MONITOR
    - New columns at `V$SQL_MONITOR`
        - RM_LAST_ACTION: Action taken by DRM. Cancel SQL or kill session
        - RM_LAST_ACTION_REASON: Reason, such as switch_io_logical or switch_elapsed_time
        - RM_LAST_ACTION_TIME: Time of Action
        - RM_CONSUMER_GROUP: Consumer Group of SQL operation

### Explain Multi-process Multi-threaded Oracle architecture 

- Requires
    - Init Para: THREADED_EXECUTION= true 
    - Default false; restart required to change
    - Cannot use OS authenication for threaded execution; Use password instead
- Oracle process executes as OS threads in separate address spaces
    - Some process are still standalone: PMON, DBW0, VKTM, PSP0
- View: `V$PROCESS` has new column SPID and STID
    - `select spid, stid, program from v$process order by 1, 2`
- Oracle recommended change to tnsnames.ora (!)
    - (!) Internal listener thread: SCMN
    - local_listener= <TNS_of_the_instance>
    - dedicated_through_broker_listener= on

### Use Flash Cache 

- Old Way: Solaris and Oracle Enterprise Linux (OEL) only
    - Recommended Flash Cache Size= 2 to 10 time size of buffer cache
    - Recommended ASM size= 2 to 10 time size of SGA
    - Flash Cache limited to one device
- New way: 
    - Up to 16 devices can be specified to Flash Cache
    - Buffer Cache with Flash Cache adds _object-based algorithm_ on top of existing _LRU algorithm_
        - allow in-memory parallel query (PQ) algorithm to takes advantage of flash cache
- Init Para
    - db_flash_cache_file= /dev/raw/sda, /dev/raw/sdb
    - db_flash_cache_size= 32G, 64G
    - View in `V$SPPARAMETER`
    - Can temporarily disable a flash cache by setting size to 0
    - Can enable flash cache by restoring original size
        - **Cannot** change device or size other than original value
- In-memory PQ algorithm
    - Requires: PARALLEL_DEGREE_POLICY= AUTO or ADAPTIVE
        - Automatic degree of parallelism (AutoDOP)
    - New statistics measure when using object-based algorithm
        - Data warehouse scanned chunks = Nbr of 1MB chunks scanned in-memory PQ
        - Data warehouse scanned chunks- disk = Nbr of chunks scanned from direct disk read
        - Data warehouse scanned chunks- flash = Nbr of chunks scanned from flash cache
        - Data warehouse scanned chunks- memory = Nbr of chunks scanned from buffers in memory
        - Data warehouse scanned objects = Nbr of objects scanned in-memory PQ

## Index and Table Enhancements
### Use Index enhancements 

- Multiple Index on Same set of column: One of following must be true
    - Index must be different types
        - Cannot create B-tree index and Clustered B-tree index
        - Cannot create B-tree index and Index-organized table (!)
    - Index must use different partition types
        - partitioned index and non-partitioned index are different 
        - global and local index are different
    - Unique and non-unique index are different
- While Multiple Index are created
    - At most one of them can be visible at any time
        - Only save time so no need to drop and recreate index
    - Optimizer only pick visible index
        - Override by Init Para `OPTIMIZER_USE_INVISIBLE_INDEXES`=true (!)
    - SQL
        - `alter index ord_customer_ix01 invisible`
        - `alter index ord_customer_ix01 visible`

### Use Table enhancements 

- Invisible column
    - Aim: Enable application enhancements without affecting existing application functions
    - Need to explicitly specify at select or insert
        - Insert without invisible column results in ORA-913 too many values error
    - Invisible at `SELECT * FROM`
    - Invisible columns are not described
        - Except `SET COLINVISIBLE ON | OFF`
    - Invisible column can be partition key or virtual column
        - Only implicit user query cannot see that
    - Virtual column can be turned Invisible
    - Cannot turn system generated **hidden** column visible: They are hidden on purpose
        - View `USER_TAB_COL` Column `HIDDEN` and `USER_GENERATED`
    - SQL
        - `alter table test_lab1 add nickname varchar2(20) invisible`
        - `alter table test_lab1 modify nickname visible`
    - Not allowed in:
        - External Table
        - Cluster Table
        - Tempoary Table

### Use Online operation enhancements 

- Online Redefinition of table on VPD
    - Argument `COPY_VPD_OPT` on `DBMS_REDEFINITION.START_REDEF_TABLE()`:
        - NONE : Default and state no VPD policy enabled; Procedure return error if the table has VPD policy
        - CON_VPD_AUTO : **Package** to copy VDB Policy to new table during online redefinition
        - CON_VPD_MANUAL : **Manually** copy VDB Policy to new table during online redefinition
            - Requires when there are column mapping between original table and interim table
            - Requires when VPD policy needs to add or modify during online redefinition
            - In either case DBA must specify modified VPD policy for interim table before `START_REDEF_TABLE()`
        - Example of CON_VPD_AUTO
```
        exec DBMS_REDEFINITION.START_REDEF_TABLE( 
            uname=> 'hr', orig_table=> 'employees', int_table=> 'init_employees',  
            options_flag=> DBMS_REDEFINITION.con_use_pk, copy_vpd_opt=> DBMS_REDEFINITION.con_vpd_auto 
        )
```
- DML timeout on Online Redefinition
    - Argument `DML_LOCK_TIMEOUT` on `DBMS_REDEFINITION.FINISH_REDEF_TABLE()`: Nbr of seconds
    - On timeout, the procedure stop to wait for DML locks and abort
    - 0 (default)= No wait and abort immmediately on failure to lock
    - NULL or 1000000 = No timeout and wait indefinitely
        - Need `ABORT_REDEF_TABLE()` to stop

- New online DDL capability
    - In all cases below DDL can be run in parallel to DML
    - Drop index and partitioned index online `drop index id01 online`
    - Drop constraint online `alter table employees drop contrainst emp_email_uk online`
    - Alter index unusable `alter index id01 unusable online`
    - Set column unused `alter table employees set unused ename online`

## Backup, Recovery and Flashback for a CDB/PDB
### Perform backup of CDB and PDB 

- System privilege for backup: SYSBACKUP (as well as SYSDBA)
- Backup for whole CDB
    - backup database
    - restore database
    - recover database
- Backup only for PDB _as common user_
    - backup pluggable database pdb1 (,pdb2)
    - restore pluggable database pdb1
    - recover pluggable database pdb1
    - backup pluggable database ''CDB$ROOT''
        - Also backup database root;
- Backup only PDB as local user
    - backup database
- Column PLUGGABLE_DBID available for V$_ and RC_ views stored at controlfile
    - RC_PDBS stores recovery catalog information
- Archivelog mode and Control file owned only by CDB
    - Backup PDB won't backup archivelog
- Backup Controlfile: `ALTER DATABASE BACKUP CONTROLFILE TO TRACE`
- Backup include SPFILE and ARCHIVELOG: 
    1. `connect target /`
    1. `configure controlfile autobackup on;`
    1. `backup database plus archivelog delete input;`
- Backup can be made with _backup sets_ or _image copies_
- User managed backup (not RMAN) of CDB
    1. alter database begin backup;
    1. (Copy database files by OS command) 
    1. alter database end backup;
- User managed backup (not RMAN) of PDB by common user
    1. alter pluggable database pdb1 begin backup;
    1. (Copy PDB datafiles by OS command) 
    1. alter pluggable database pdb1 end backup;
- Backup tablespace
    - backup tablespace system, pdb1:system;
        - But it is better to connect to PDB to backup its tablespace to avoid naming ambiguity
        - backup datafile has no such ambiguity because datafile number and path are both unique

### Perform recovery of CDB and PDB 

- General recovery rules
    - Crash recovery must be done at CDB level; No crash recovery only for PDB
    - Flashback a common schema will flashback across whole CDB
    - Media recovery allowed at PDB corruption
    - PITR allowed on PDB
- Crash recovery without media corruption
    1. Connect to root
    1. Startup database
    1. Open all PDBs (when they are mounted only) 
    - Below are done during the crash recovery
    1. Redo log at applied for whole CDB
    1. Rollback uncommitted changed in root containers
    1. Rollback uncommitted changed in PDBs (when opening PDBs)
- Complete recovery for whole CDB
    - (controlfile and SPFILE intact, database in mount mode)
    1. restore database;
    1. recover database;
- Complete recovery on root container only
    - Oracle recommends to recover whole CDB instead root container only to avoid metadata inconsistency
    - (controlfile and SPFILE intact, database in mount mode)
    1. restore database root;
    1. recover database root;
    1. restore pluggable database ''PDB$SEED'', pdb1, ...;
    1. recover pluggable database ''PDB$SEED'', pdb1, ...;
    1. alter database open;
    1. alter pluaggable database all open;
- Perform complete recovery for PDB without affecting other PDB
    - As common SYSBACKUP
        1. alter pluggable database pdb1 close;
        1. restore pluggable database pdb1;
        1. recover pluggable database pdb1;
        1. alter pluggable database pdb1 open;
    - As local SYSBACKUP
        1. alter pluggable database close;
        1. restore database
        1. recover database
        1. alter pluggable database open;
- Media recovery
    - Losing controlfile
        1. startup nomount;
        1. restore controlfile from autobackup;
        1. alter database mount;
        1. (Continue database recovery)
        1. alter database open resetlogs;
        1. alter pluaggable database all open;
    - Losing redo log
        - same as non-CDB
    - Losing CDB or PDB temporary file
        - Temp file of CDB will be re-created automatically (and use as default)
        - Temp file of PDB to be re-created manually
    - Losing undo or system datafile under root container
        1. (controlfile and SPFILE intact or recovered, database in mount mode)
        1. restore tablespace xxx;
        1. recover tablespace xxx;
        1. alter pluaggable database all open;
    - Losing sysaux datafile under root container
        - `alter tablespace sysaux online` after it is recovered
    - Losing PDB system datafile
        1. (Change PDB to mounted state)
        1. restore tablespace pdb1:system;
        1. recover tablespace pdb1:system;
    - Losing PDB non-system datafile
        1. (Offline corrupted tablespace) `alter tablespace users offline immmediate;`
        1. restore tablespace pdb1:users;
        1. recover tablespace pdb1:users;
        1. `alter tablespace users online;`
- PITR
    - Flashback is easier than PITR
        - But cannot Flashback beyond flashback retention period
    - Carry out PITR on PDB only affect that PDB
        - The PDB to be open with RESETLOGS
        - CDB incarnation number not changed. 
        - PDB incarnation is changed to (1,2), rather then 2 like non-CDB.
    - Example (Use function `timestamp_to_scn()` to identify scn)
```
    run {
        set until scn= 1234567;
        restore pluggable database pdb1;
        recover pluggable database pdb1;
        auxiliary destination= '/u01/app/oracle/backup_dir';
        alter pluggable database pdb1 open resetlogs;
    }
```

### Perform Flashback for a CDB 

- Requires (no change)
    - Enable Fast Recovery Area (FRA)
    - Set flashback retention target
    - Enabled flashback database
- Multitenant rules
    - Cannot flashback root container only; Must flashback entire CDB to flashback root container
    - Cannot flashback to a point earlier than PITR at CDB or any PDB 
- Flashback CDB
    1. Startup in exclusive mode `startup mount exclusive`
    1. Set flashback retention target in minutes `alter system set db_flashback_retention_target=2880 scope=both`
    1. Set flashback `alter database flashback on`
    1. Open database `alter database open`
    1. Confirm some data exists
    1. Get current SCN `select current_scn from v$database`
    1. Delete that data
    1. Switch log `alter system switch logfile` (x3)
    1. Shutdown `shutdown immediate`
    1. `startup mount`
    1. Flashback to SCN when data still exists `flashback database to scn nnn`
    1. `alter database open resetlogs`
    1. `alter pluggable database all open`
- Flashback CDB after PITR: Take all files of the PDB having PITR offline
    1. Find SCN or time that need to flashback
    1. Take all PDB files that done PITR offline `alter pluggable database pdb2 datafile all offline`
    1. Flashback to SCN required `flashback database to scn nnn`
    1. `alter database open resetlogs`
    1. `restore pluggable database pdb1`
    1. `alter pluggable database pdb2 datafile all online`
    1. `recover pluggable database pdb1`
    1. `alter pluggable database pdb2 open`

## RMAN and Flashback Data Archive
### Use RMAN enhancements 

- New system privilege: SYSBACKUP: Local user can be granted to SYSBACKUP
- Local user can use `BACKUP DATABASE` but not `BACKUP PLUGGABLE DATABASE`
- Use SQL in RMAN
    - When connect to older database
        - SQL Prefix still required to earlier database with quoting `SQL 'alter system switch logfile'`
    - When connect to 12c database
        - SQL quotes are permitted but not required
        - SQL statement newly supported in 12c
            - SELECT
            - ALTER TABLESPACE
            - CREATE DIRECTORY
        - SQL Prefix no required to connect 12c database, except (!)
            - SQL DELETE 
            - SQL DROP DATABASE
            - SQL FLASHBACK
        - SQL can be used within run block with quotes (!)
```
        run {
            SQL "alter tablespace users offline immmediate";
            restore tablespace users;
            recover tablespace users;
            SQL "alter tablespace users online";
        }
```
- Multisection backup of Image Copies
    - Old way: Multisection backup only available for backupsets
    - New way: SECTION SIZE supports image copy
    - New way: SECTION SIZE supports incremental backup
    - Requires: COMPATIBILE >= 12.0.0
    - `BACKUP AS COPY SECTION SIZE 500m DATABASE`
    - Performance Concern: Avoid big parallelism of multisection backup on small number of disk
- Duplication enhancements
    - By default, 12c RMAN duplicate database from backupset
    - Can end duplication of database in database mount state
    - Can choose compression, encryption and section size
    - Active Duplication
        - Old way Push based: send image copy from source database to auxiliary database over network
        - New way Pull based: pull backupset from source database
            - Less stress to source database
        - Use pull based when:
            - `DUPLICATE DATABASE USING BACKUPSET`
            - `DUPLICATE DATABASE USING COMPRESSED BACKUPSET`
            - `SET ENCRYPTION` before `DUPLICATE`
            - `DUPLICATE` having `SECTION SIZE` clause
            - `DUPLICATE` having `FROM ACTIVE DATABASE` clause
        - Encryption at Duplication
            1. Share Oracle Keystore between source and auxiliary database
            1. `SET encryption on identified by <password>`
            1. `CONNECT TARGET "xxx@src AS SYSBACKUP"`
            1. `CONNECT AUXILIARY "xxx@dst AS SYSBACKUP"`
            1. `SET ENCRYPTION ALOGRITHM "AES128'`
            1. `DUPLICATE TARGET DATABASE TO dst FROM ACTIVE DATABASE PASSWORD FILE`
        - Compressed Backupset Duplication
            - `DUPLICATE TARGET DATABASE TO dst FROM ACTIVE DATABASE PASSWORD FILE USING COMPRESSED BACKUPSET`
        - Multisection Duplication with Parallelism
            - `DUPLICATE TARGET DATABASE TO dst FROM ACTIVE DATABASE PASSWORD FILE SECTION SIZE 500M`
        - No Open after Duplication
            - Some case upgrade scripts are carried out after duplication. Prefer not to OPEN database
            - OPEN RESETLOGS later
            - `DUPLICATE TARGET DATABASE TO dst FROM ACTIVE DATABASE NOOPEN`
    - Can duplicate CDB, PDB and non-CDB
        - Duplicate CDB (!)
            1. Backup CDB (!)
            1. Add information for duplicate database at tnsnames.ora and listener.ora
            1. Create Init file for duplicate database
                - Make sure ENABLE_PLUGGABLE_DATABASE=true for CDB
            1. Start auxiliary instance (cdb2)
            1. Connect RMAN to root container of auxiliary instance target
            1. `backup copy of database`
                - When copy not available:  RMAN-06585: no copy of datafile 1 found 
            - (!) where is the duplicate command used? Missing Step?
        - Duplicate PDB (!)
            - Duplicated database will contain root container, seed container and specified PDB
            - Can duplicate list of PDB or duplicate all PDBs with an exception list
            1. Add information for duplicate database at tnsnames.ora and listener.ora
            1. Create Init file for duplicate database
            1. Start auxiliary instance (cdb2)
            1. Connect RMAN to **root container** of auxiliary instance target
            1. `backup copy of pluggable database pdb1, ...(list)`
                - When copy not available:  RMAN-06585: no copy of datafile 1 found 
            1. `DUPLICATE DATABASE to cdb2 pluggable database pdb1, ...(list)`
        - Duplicate Tablespace
            - Duplicate specific TS: `DUPLICATE DATABASE to cdb2 tablespace pdb1:users`
            - Duplicate PDB and specific TS `DUPLICATE DATABASE to cdb2 pluggable database pdb1 tablespace pdb2:users`
- Transportable Tablespace by Backupset
    - Summary
        - Backupset can be compressed or transport by multisection
        - Cross platform backupset view: `V$TRANSPORTABLE_PLATFORM`
        - `ALLOW INCONSISTENT` to transport inconsistent tablespaces for both image copy or backupset
    - Transport Database to different platform via backupset
        1. Check whether this database (in specific state) can be transported to target platform 
            - `select user from dual where DBMS_TDB.CHECK_DB('Microsoft Windows IA (32-bit)', DBMS_TDB.skip_readonly)`
            - Results of `DBMS_TDB.CHECK_DB` is boolean; Do not proceed in case of false (no row returned)
        1. `ALTER DATABASE open read only`
        1. `BACKUP TO PLATFORM 'Microsoft...' FORMAT '/...' DATABASE`
            - Platform and filename specific
                - TO PLATFORM 'Microsoft Windows IA (32-bit)'
                - FORMAT '/u02/app/oracle/oradata/trans1_%u'
                - Backupset output filename '/u02/app/oracle/oradata/trans1_0aos32er_1_1'
        1. SFTP backupset to destination server using OS utility
        1. destination rman `CONNECT target sysbackup@orcl2 as sysbackup`
        1. `RESTORE FOREIGN DATABASE TO NEW FROM BACKUPSET '/...'`
            - TO NEW: OMF 
            - Platform and filename specific
                - FROM BACKUPSET '/u02/app/oracle/oradata/trans1_0aos32er_1_1'
    - Transport Tablespaces to different platform via backupset
        1. source rman `CONNECT target sysbackup@orcl1 as sysbackup`
        1. `ALTER TABLESPACE test READ ONLY`
        1. Prepare output filename by backup command
            - FORMAT clause: DBA supplied format
            - TO NEW clause: OMF and always unique
        1. Gather **exact platform name** and check endian difference
            - `select platform_id, platform_name, endian from V$TRANSPORTABLE_PLATFORM (WHERE ...)`
        1. `BACKUP TO PLATFORM 'Linux...' FORMAT '/...' DATAPUMP FORMAT '/...' TABLESPACE test`
            - RMAN does not catalog this backup
            - Backup located at export folder at source database
                - This is the file to be transported
            - `TO PLATFORM` specify endian conversion done at source
                - `FOR TRANSPORT` specify endian conversion done at destination
            - Platform and filename specific 
                - TO PLATFORM 'Linux x86 64-bit'
                - FORMAT '/u02/app/oracle/oradata/trans1_%u'
                - Backupset output filename: '/u02/app/oracle/oradata/trans1_06os30m5'
                - DATAPUMP FORMAT '/u02/app/oracle/export/trans1_%u'
                - Datapump output filename: '/u02/app/oracle/export/trans1_07os30m7_1_1'
        1. SFTP backupset and export file to destination server using OS utility
        1. destination rman `CONNECT target sysbackup@orcl2 as sysbackup`
        1. `RESTORE FOREIGN TABLESPACE test FORMAT '/...' FROM BACKUPSET '/...' DUMP FILE FROM BACKUPSET '/...'`
            - Platform and filename specific 
                - BACKUPSET '/u02/app/oracle/oradata/trans1_06os30m5'  (DirPath at destination OS)
                - DUMP FILE FROM BACKUPSET '/u02/app/oracle/export/trans1_07os30m7_1_1'  (DirPath at destination OS)
                - FORMAT '/u02/app/oracle/oradata/orcl2'  (align to other oracl2 datafile)
                    - FORMAT can be overriden by TO NEW
                    - FORMAT can be overriden by Init Para DB_CREATE_FILE_DEST
- Table Recovery
    - Old way: DBPITR export/import
    - Flashback as alternative; but cannot flashback a purged/truncated table or some other reason
    - New way: Table Recovery can recover a table(s) or table partition(s)
    - PITR option:
        - UNTIL SCN: `timestamp_to_scn()`
        - UNTIL TIME: Format NLS_LANG or NLS_DATE_FORMAT
        - UNTIL SEQUENCE: log sequence and thread number
    1. rman `connect target /`
    1. `RECOVER TABLE employees UNTIL SCN 1234567`
        1. RMAN creates an auxiliary instance
            - Can be specified by `AUXILIARY DESTINATION` clause (recommended) or `NEW NAME` clause
            - RMAN select a location if not specified
        1. RMAN recover table up to SCN into auxiliary instance
        1. RMAN create a datapump export file with recovered table data
            - Datapump file can be specified by `DATAPUMP DESTINATION` clause
            - RMAN use OS specific location if not specified
    - Tables or Partitions can be renamed by REMAP TABLE clause or REMAP TABLEPSACE clause (!)
    - (!) Whether pump file is imported to database?

### Implement the new features in Flashback Data Archive (FDA)

- FDA for security related application tables
    - Can get full history all security related application tables with a single command
    - Track their changes for audit requirement
    - Can change security related application table to readonly with a single command

- User-Context Tracking
    - Track transaction by metadata: including user-context
    - identify user who change a table

- Hybrid Columnar Compression (HCC) on Exadata
    - FDA can be used on HCC compressed tables

- History Import and Export
    - Import user-generated history into FDA tables

- FDA History Table Optimization
    - `OPTIMIZE DATA` clause at creation of FDA to conserve storage
        - Advanced row compression
        - Advanced LOB compression
        - Advanced LOB de-duplication
        - Segment level compression tiering
        - Row level compression tiering
    - Default: `NO OPTIMIZE DATA`


## Oracle Data Pump, SQL*Loader, External Tables and Online Operations Enhancements [8]
### Use Oracle Data Pump enhancements 

- Fully Transportable Export Import
    - Concept
        - Fully transportable export= export all objects and data needed to create a copy of database
        - Fully transportable import= import dump and create the database
        - Parameter: `FULL=Y`, `TRANSPORTABLE=ALWAYS` and `VERSION=12.0`
            - FULL=Y: Export full database except Oracle internal schema
            - TRANSPORTABLE=ALWAYS: Export all metadata of exported objects
            - VERSION=12.0 or higher as required to use
    - Use cases
        - Upgrade database from 11.2.0.3 or above
        - Transport from non-CDB to CDB
        - Transport across platform
    - Limitation
        - Does not support auditing on SYSTEM/SUSAUX tablespace
        - Does not support table with LONG RAW or LONG column
        - When there is encrypted tablespace or column, source and target OS must have same endianness
        - When there is encrypted tablespace or column, unsupported transport over network
    - Attention
        - When there is encrypted tablespace or column, must specify ENCRYPTION_PASSWORD (!)
        - When source and target OS endian are different, must convert by
            - `DBSM_FILE_TRANSFER` or RMAN `CONVERT` command
    - Steps:
        1. Export database needs either VERSION or COMPATIBLE to 12.0 or higher
        1. Create database at target with empty data
        1. Make all user-defined tablespaces read-only
            - `ALTER TABLESPACE users READ ONLY`
        1. `expdp system FULL=Y TRANSPORTABLE=ALWAYS VERSION=12.0 dumpfile=exp.dmp directory=dp_dir logfile=expdp.log`
        1. SFTP export dump to destination server
            - Need to convert on different endianness
        1. Import by:
            - `impdp system FULL=Y TRANSPORT_DATAFILE=... dumpfile=exp.dmp directory=dp_dir logfile=impdp.log`
                - Sample: TRANSPORT_DATAFILE='/u01/app/oracle/oradata/prod/sales.dbf','/u01/app/oracle/oradata/prod/sales.dbf'
            - `impdp system FULL=Y TRANSPORT_DATAFILE=... dumpfile=exp.dmp directory=dp_dir logfile=impdp.log NETWORK_LINK=srcdb `
                - File transported over network link; No SFTP needed
    - Full transportable export move both metadata and data for obejcts in non-transportable tablespace
        - Using direct path unload and external tables

- Disable Logging at Import
    - Skip redo log for faster import
        - Good for importing data to new/empty database
        - DDL and DCL operation like CREATE TABLE, ALTER TABLE (exclude CREATE INDEX) still logged
        - If the import fails, it must be restarted
    - Parameter: 
        - `TRANSFORM=disable_archive_logging:y` : Skip logging on table and index import
        - `TRANSFORM=disable_archive_logging:y:index` : Skip logging on index import; logging on table import as default
        - `TRANSFORM=disable_archive_logging:y:index TRANSFORM=disable_archive_logging:n:table` : Same as previous
- Specify Compression at import
    - Parameter `TRANSFORM=table_compression_clause:[]` : Specify table_compression as following choice
        - NONE: Inherit compression setting of tablespace
        - COMPRESS : Shorthand of ROW STORE COMPRESS BASIC
        - ROW STORE COMPRESS BASIC : basic compression during direct path insert
        - ROW STORE COMPRESS ADVANCED : Compress during all DML operations
    - Quotes (command line) needed for spaces in parameter
    - Quotes not needed for impdp parameter file
- Specify SecureFile LOB at Import
    - Parameter `TRANSFORM=lob_storage:[]` : Specify LOB segment type
        - DEFAULT: LOB segment created with default storage setting
        - BASICFILE: BasicFile LOB segment
        - SECUREFILE: SecureFile LOB segment
        - NO_CHANGE: Default value; LOB segment same as source
- Export views as tables
    - Parameter: `VIEWS_AS_TABLES`
        - Cannot use `VIEWS_AS_TABLES` with `TRANSPORTABLE=ALWAYS`
        - Can use `VIEWS_AS_TABLES` with `TABLES`
        - Limited to views with only scalar columns, without referring functions and object types
        - May export XML data in relational format and import into a relational table
    - Examples
        - `expdp hr/<pwd> directory=dp_dir datadump=hr1.dmp VIEWS_AS_TABLES=employee_v TABLES=departments`
        - `expdp hr/<pwd> directory=dp_dir datadump=hr1.dmp VIEWS_AS_TABLES=employee_v managers_v`
        - `expdp hr/<pwd> directory=dp_dir datadump=hr1.dmp VIEWS_AS_TABLES=employee_v remap_table=employee_v:employee`
        - `expdp hr/<pwd> directory=dp_dir network_link=hr_link VIEWS_AS_TABLES=employee_v table_exists_action=append`


### Use SQL*Loader and External table enhancements 

- SQL*Loader Express Mode
    - Minimum command argument: table name (sqlldr ask for username/password)
        - Short form command sample: `sqlldr oe table=test`
        - Does not use sqlldr control file
    - Require: Table datatype can only have _character_, _number_ and _datetime_
    - Concepts
        - Log file: Output as sqlldr control file, and SQL scripts to create an external table helpful for IAS
        - Result log file: Results of sqlldr data loading process (!)
    - Assume default setting but can be overriden
        - Data file: <tablename>.data
        - Log file: <tablename>.log
        - Bad file: <tablename>_%p.bad
        - Oracle database log file: <tablename>_%p.log_xt
    - Express mode have some parameter same as regular sqlldr but _some of them behave differently_

- Identity Column and Direct Path Loading
    - Identity column: Values taken from a sequence generator `GENRATED AS ... IDENTITY clause`
        - Example: `ALTER TABLE tab1 ADD col1 NUMBER GENERATED BY DEFAULT ON NULL AS IDENTITY`
        - `GENERATED ALWAYS AS IDENTITY`
            - Column value always comes from a sequence generator
            - Explicit insert null value replaced by number from sequence generator
            - Error on explicit insert or update any value (except insert null which means sequence nbr)
            - **Does not support Direct Path Loading**
        - `GENERATED BY DEFAULT AS IDENTITY`
            - Column value **by default** comes from a sequence generator
            - Can explicit insert or update value
            - **Does not support Direct Path Loading**
        - `GENERATED BY DEFAULT ON NULL AS IDENTITY`
            - Column value by default comes from a sequence generator at assign it to null
            - Can explicit insert or update value
            - **Support Direct Path Loading**

- Syntax Enhancements for SQL*Loader and External Table
    - Data filename can use wildcard (* and ?)
    - Support CSV with embedded newlines: `FIELDS CSV WITH EMBEDDED`
    - Table-level `NULLIF` and `DATE FORMAT` can be specified once on all character and date fields
        - FIELDS DATE FORMAT "DD-MMM-YYYY" 
        - FIELDS TERMINATED BY "," NULLIF "NA"
    - Can specify `FIELD NAMES` clause and include name and order of fields (!)
    - On External tables, can specify `ALL FIELDS OVERRIDE` for default attribute of columns
        - So you can specify only the column that don't match the default

## Partitioning Enhancements  [8] 
### Explain Partitioning enhancements 

- Online Partition Operations
    - Move partition online `ALTER TABLE MOVE PARTITION ... ONLINE`
        - Operation completes after DML started before the operation completes
        - Include `UPDATE INDEXES` clause so no need to rebuild later
            - Both global and local indexes are maintained online
        - Sample: `ALTER TABLE sales MOVE PARTITION sales_p1 TABLESPACE lowtbs UPDATE INDEXES ONLINE`
        - Sample: `ALTER TABLE sales MOVE PARTITION sales_p1 COMPRESS BASIC UPDATE INDEXES ONLINE`
    - Compression levels
        - COMPRESS BASIC
        - COMPRESS ADVANCED (old name COMPRESS FOR OLTP)
        - COMPRESS FOR QUERY [HIGH | LOW] : Compression for partitions expecting no DML
        - COMPRESS FOR ARCHIVE [LOW | HIGH] : HCC, Hybrid Columnar Compression

- Reference Partitioning with parent table as Interval Partitioning
    - New: Interval Partitioned table can be parent of Reference Partitioning
        - Interval Partition is a subtype of Range partition with Interval defined
        - Reference partition name inherits from Parent table
        - Reference partition inherits Parent table tablespace allocation _unless_ other specified
        - `SPLIT PARTITION` AT parent cascade to reference table
    - New: CASCADE option for TRUNCATE partition and EXCHANGE partition at parent table
        - Apply to `TRUNCATE TABLE`, `ALTER TABLE TRUNCATE PARTITION`, `ALTER TABLE TRUNCATE SUBPARTITION`
        - Apply to `ALTER TABLE EXCHANGE PARTITION`, `ALTER TABLE EXCHANGE SUBPARTITION`
        - Sample: `TRUNCATE TABLE oe.orders CASCADE`
        - Effect: Records of child table are truncated **recursively**
        - Other effects like `UPDATE INDEXES` are affected by CASCADE; Index of affected table are updated

- Multiple Partition Maintenance Operations
    - Add multiple partitions
        - Support add multiple range, list or system partition to a table
        - Support add multiple range or list subpartition to a partition
        - When adding multiple ranged partitions, SQL must list partitions in ascending order and cannot add MAXVALUE partition
        - When adding multiple list partition, SQL cannot add DEFAULT partition
        - Sample: `ALTER TABLE sales ADD PARTITION sales2013q1 VALUES LESS THAN date'2013-04-01' PARTITION sales2013q2 VALUES LESS THAN date'2013-07-01' PARTITION sales2013q3 VALUES LESS THAN date'2013-10-01'`
    - Truncate multiple partitions
        - Support truncate multiple range or list partition
        - Sample: `ALTER TABLE sales TRUNCATE PARTITION sales2013q1, sales2013q2, sales2013q3`
        - Absence of UPDATE INDEXES clause
            - Local indexes are usable for remaining partitions; Global index needs rebuild
    - Merge multiple partitions
        - Support merge multiple range, list or system partition
        - Support merge multiple range or list subpartition
        - When merge multiple ranged partitions
            - SQL must list partitions adjacently in ascending order
            - SQL may list partitions using TO keyword
        - When merge multiple list partition with a DEFAULT partition, results is a DEFAULT partition
        - Sample `ALTER TABLE sales MERGE PARTITION sales2013q1 TO sales_2013q3 INTO PARTITION sales2013`
    - Split multiple partitions
        - Support split range or list partition into multiple multiple partitions
        - Range partition: Specify N-1 values to split into N partitions
        - List partition: Specify N-1 literals to split into N partitions
        - MAXVALUE (range) and DEFAULT (list) partition: Last partition of split remains as MAXVALUE and DEFAULT partition
        - Sample: `ALTER TABLE sales SPLIT PARTITION sales2013 INTO PARTITION sales2013q1 VALUES LESS THAN date'2013-04-01' PARTITION sales2013q2 VALUES LESS THAN date'2013-07-01' PARTITION sales2013q3 VALUES LESS THAN date'2013-10-01' PARTITION sales2013q4`
    - Drop multiple partitions (!)
        - Sample: `ALTER TABLE sales DROP PARTITION sales2013q1, sales2013q2, sales2013q3`

### Explain Index enhancements for partitioned tables

- Partial Index
    - Create local or global index on a subset of table partition or subpartition
    - Default: INDEXING FULL; Special: INDEXING PARTIAL
        - By default ALL global indexes cover all partition and local indexes are USABLE
    - Example of `INDEXING` clause
```
    CREATE TABLE orders (
        order_id number(9),
        order_date date constraint order_date_nn not null,
        order_total number(12)
        INDEXING OFF
        PARTITION BY RANGE (order_date)
        PARITTION ord12 VALUES LESS THAN date'2013-01-01' INDEXING ON
        PARITTION ord13 VALUES LESS THAN date'2014-01-01' INDEXING OFF
        PARITTION ord14 VALUES LESS THAN date'2015-01-01' INDEXING ON
        PARITTION ord15 VALUES LESS THAN date'2016-01-01' 
    )
```
    - In example above:
        - All partial global indexes covers ord12 and ord14
        - All partial local indexes created on ord12 and ord14 are USABLE
        - All partial local indexes created on ord13 are UNUSABLE as specified
        - All partial local indexes created on ord14 are default to UNUSABLE
    - Example of Index creation:
        - Create global partial index `CREATE INDEX ord_ix01 ON orders(order_total) GLOBAL INDEXING PARTIAL`
        - Create local partial index `CREATE INDEX ord_ix01 ON orders(order_total) LOCAL INDEXING PARTIAL`
        - Create global full index `CREATE INDEX ord_ix01 ON orders(order_total) GLOBAL INDEXING FULL`
    - Change to columns on Index related DataDic:
        - `USER_INDEXES`: new column `INDEXING`= [ PARTIAL | FULL ]
        - `USER_IND_PARTITION`: existing column `STATUS`= [ USABLE | UNUSABLE ] evaluated as above
        - `USER_PART_TAB`: new column `DEF_INDEXING` = [ ON | OFF ] at table level 
        - `USER_TAB_PARTITION`: new column `DEF_INDEXING` = [ ON | OFF ] at partition
        - `USER_TAB_SUBPARTITION`: new column `DEF_INDEXING` = [ ON | OFF ] at partition

- Asynchronous Global Index
    - Global index are Asynchronously maintained
        - Only metadata adjusted at DROP PARTITION or TRUNCATE PARTITION
        - Index entries remains (Orphaned), but invalid and ignored
        - Global indexes are USABLE (was UNUSABLE in old ways)
        - UPDATE INDEXES clause available to DROP PARTITION or TRUNCATE PARTITION for _backward compatibility_
    - Exception
        - Table owned by SYS
        - Table with domain index
        - Table with object types
    - Orphaned Index entries
        - New column `ORPHANED_ENTRIES` in `DBA_INDEXES` and `DBA_IND_PARTITIONS` values [ YES | NO | NA ]
        - Clean up Orphaned entries by `DBMS_PART.CLEANUP_GIDX()`
        - Scheduled Job `PMO_DEFERRED_GIDX_MAINT_JOB` runs _nightly_ to invoke `DBMS_PART.CLEANUP_GIDX()`
            - Can be invoked by `DBMS_SCHEDULER.RUN_JOB()`
        - SQL: `ALTER INDEX COALESCE CLEANUP` and `ALTER INDEX REBUILD` also remove Orphaned entries


## Information Lifecycle Management and Storage Enhancements 
### Use ILM features 
- Lifecycle Management: regulatory requirement on data lifetime
    - Some data must be key retention for compliance requirement
    - Tools used for ILM policy: **Oracle Partitioning**, **Data Compression**, **Multi-Tier Storage**
        - In-database solution
    - Once data get old and rarely modified or accessed
        - Compressed Advanced (Compress for OLTP) for data still needed on OLTP
        - Move partition to lower-cost storage tier for less accessed data
        - Move partition to Hydrid Columnar Compression (HCC) for strong Compression
    - 12c allow automation of ILM policy implementation
        - In 11g ILM policy implementation is manual process only, and tedious
    - Concepts
        - Heat Map statistics: Identify which data is hot and cold (modified and accessed)
        - Automatic Data Optimization (ADO): Process to propose and create ILM policy by Heat Map data
        - Temporal Validity: Valid time dimension to indicate operation relvance
        - In-Database Archiving: Archive dormant rows alongside with operational and valid rows

### Perform tracking and automated data placement 

- Automatic Data Optimization (ADO)
    - Data Lifecycle
        - Active Data: newly inserted or actively update data; Advanced Row Compression
        - Frequent Accessed: Frequently accessed but not Active Data; High Compression at high performance storage
        - Infrequent Accessed: Infrequently accessed; High Compression at low performance storage
        - Dormant data: Kept only for purpose of compliance; Archive Compression at cheap storage or tape storage
    - ADO flow
        1. Enable Heat Map
        1. Create ADO Policy
        1. Scheduled ADO Policy evaluation
        1. Review ADO evaluation results at `DBA_ILM_EVALUATIONDETAILS` and `DBA_ILMRESULTS` (!)
        1. Verify compression of block and segments at `COMPRESSION_STAT$` and whether segments moved to intended TBS
    - Enable Heat Map: Init Para `HEAT_MAP`= ON (OFF default)
        - Views:
            - Heat Map Data: `DBA_HEAT_MAP_SEGMENT` and `DBA_HEAT_MAP_SEG_HISTOGRAM`
            - Heat Map by TBS: `DBA_HEATMAP_TOP_TABLESPACES`
            - Heat Map realtime data: HEAT_MAP_STAT$ and `V$HEAT_MAP_SEGMENT`
            - Clear realtime Heat Map: `DBMS_ILM_ADMIN.CLEAR_HEAT_MAP_ALL()`
        - DBA_HEAT_MAP_SEG_HISTOGRAM columns:
            - TRACKED: Time when segment _tracked_
            - SEGMENT_WRITE: whether segment accessed for write
            - SEGMENT_READ_TIME: Last Time when segment read
            - SEGMENT_WRITE_TIME: Last Time when segment accessed for write
            - FULL_SCAN: whether segment accessed for full scan
            - LOOKUP_SCAN: whether segmenta accessed for lookup scan
        - Package `DBMS_HEAT_MAP` (!)
            - BLOCK_HEAT_MAP function: returns heat map at block level
            - EXTENT_HEAP_MAP function: returns heat map at extent level
            - OBJECT_HEAT_MAP procedure: return summary of heap map over object
            - SEGMENT_HEAT_MAP procedure: return summary of heap map over segment
            - TABLESPACE_HEAT_MAP procedure: return summary of heap map over tablespace
            - `SELECT segment_name, tablespace_name, block_id, writetime FROM TABLE(DBMS_HEAT_MAP.BLOCK_HEAT_MAP('OE','ORDERS'))`
            - `SELECT segment_name, block_id, blocks, max_writetime FROM TABLE(DBMS_HEAT_MAP.EXTENT_HEAT_MAP('OE','ORDERS'))`
    - ADO Policy
        - ADO policy level: ROW, SEGMENT, GROUP or TABLESPACE (as default policy) (!)
        - `ILM` clauses at `CREATE TABLE` and `ALTER TABLE` manage ADO policy
            - Add/delete ILM policy, Enable/Disable ILM policy
            - Policy action include Compression and storage tiering
        - Condition and Timing when ILM policy take effect
            - Condition
                - `LOW ACCESS` or `NO ACCESS`
                - `NO MODIFICATION`
                - (!) Object or row creation
                - (!) Tablespace fullness
            - Timing
                - `AFTER _nbr_ [ DAY | MONTHS ] OF`
        - ILM policy action (one of them)
            - Compression
                - ROW STORE COMPRESS [ BASIC | ADVANCED ]: Advanced better than BASIC but requires license
                - COLUMN STORE COMPRESS FOR QUERY [ HIGH | LOW ]: HCC feature; Default High
                - COLUMN STORE COMPRESS FOR ARCHIVE [ HIGH | LOW ]: HCC feature; Default Low
                - Query and Archive not available for Row level Policy
            - Move storage Tier
                - TIER TO [ tablespace ]
        - SQL Example
            - `CREATE TABLE sales_ado (...) ILM ADD POLICY COLUMN STORE COMPRESS FOR ARCHIVE HIGH SEGMENT AFTER 12 MONTHS OF NO ACCESS`
            - `ALTER TABLESPACE tbs1 DEFAULT ILM POLICY ROW STORE COMPRESS ADVANCED SEGMENT AFTER 30 DAYS OF LOW ACCESS`
            - `ALTER TABLE tab1 ILM POLICY ROW STORE COMPRESS FOR ADVANCED GROUP AFTER 90 DAYS OF NO MODIFICATION`
            - `ALTER TABLE tab1 ILM POLICY ROW STORE COMPRESS FOR ADVANCED ROW AFTER 30 DAYS OF NO MODIFICATION`
            - `ALTER TABLE tab1 MODIFY PARTITION p1 ILM POLICY TIER TO low_cost_tbs`
                - Partition move at fullness of original tablespace; Default 85% can be overriden
        - Custom ILM policy
            - `ALTER TABLE tab1 MODIFY PARTITION p1 ILM POLICY TIER TO low_cost_tbs ON MY_CUSTOM_ILM_RULE`
            - MY_CUSTOM_ILM_RULE() is a function (custom made) return true
            - Cannot combine Custom ILM policy and non-custom ILM policy
            - Custom ILM policy **must be SEGMENT level**
        - Multiple ILM policy on same segment
            - Their policy condition must be on same statistics. Only differ by Timing
            - Policy will be implemented based on timing
            - Policy will not be implemented to lower compression level
        - Enable/ Disable/ Delete ILM Policy
            - `ALTER TABLE tab ILM DISABLE_ALL`
            - `ALTER TABLE tab ILM ENABLE_ALL`
            - `ALTER TABLE tab ILM DELETE_ALL`
            - `ALTER TABLE tab ILM DELETE POLICY <name>`
        - ILM policy inheritence
            - Table ILM policy inherits Tablespace ILM policy if there is no table ILM policy
            - Table ILM policy is preferred to Tablespace ILM policy
            - `DBA_ILMOBJECTS` to check inheritence
        - Monitoring ILM policy
            - `DBA_ILMPOLICIES` to check whether policy is enabled
            - `DBA_ILMDATAMOVEMENTPOLICIES` to check data movement policy (!)
        - Evalution and and Execution of ILM Policy
            - MMON evaluates row level policy every 15 minutes
            - `DBMS_ILM.EXECUTE_ILM_TASK` evaluates segment level policy nightly
                - Evaluation interval changable by `DBMS_ILM_ADMIN.CUSTOMER_ILM`
            - `DBMS_ILM.STOP_ILM` stop execution of ILM policy
    - Viewing and Execution of ILM task
        - `DBMS_ILM.PREVIEW_ILM`: View evaluation results
            - Argument `ILM_SCOPE` => SCOPE_DATABASE and SCOPE_SCHEMA
            - This task is inactive by default
        - `DBMS_ILM.EXECUTE_ILM_TASK`: Execute ILM tasks
        - `DBMS_ILM.EXECUTE_ILM`: (!)
        - View `DBA_ILMTASKS` (!)
        - View `DBA_ILMEvalutionDetail` Column `SELECT_FOR_EXECUTION`
        - Evalution not passed with reasons:
            - Precondition not satisfied
            - Policy disabled
            - Policy overruled
            - Inherited Policy overruled
            - Job already existed
            - No operation since last ILM action
            - Target compression not higher than current
            - Statistics (Heat Map) not available
        - View `DBA_ILMRESULTS` (!)
    - Disable/ Enabled ILM entirely
        - `exec DBMS_ILM_ADMIN.DISABLE_ILM`
        - `exec DBMS_ILM_ADMIN.ENABLE_ILM`
        - `SELECT value FROM DBA_ILMPARAMETERS WHERE NAME='ENABLED'`
            - 1 is enabled, 2 is disabled
        - Disable ILM entirely is NOT disable or delete ILM policy
            - If ILM is enabled later, ILM policy will be enforced

### Move a data file online 
- Datafile are moved online: No need to put datafile offline first
    - Sample: No ONLINE keyword 
        - `ALTER DATABASE MOVE DATAFILE '/u01/app/oradata/test/data1.dbf' TO '/u02/app/oradata/test/data1.dbf'`
        - `ALTER DATABASE MOVE DATAFILE 99 TO '+diskgroup2'`
    - Move progress can be tracked by `V$SESSION_LONGOPS`
        - Progress changes: NORMAL > COPYING > SUCCESS > NORMAL
- Refer to section "Online Partition Operations" for moving partition for compression
    - which help ADO and ILM policy

## In-Database Archiving and Valid-Time Temporal

### Use In-Database archiving 

- Hybrid Columnar Compression (HCC)
    - Requires specialize storage: Exadata, ZFS or Pillar Axiom 600
    - Store data in column and compressed
        - Low cardinality columns can be heavily compressed
    - Warehouse compression
        - 10x Compression ratio
        - Support Faster Queries
    - Archive compression
        - 15x to 50x Compression ratio
- In-database archiving
    - Keep archived data and operation data together
    - Row activeness
        - Some rows are active and others are inactive
        - Inactive data can be invisible for some application
            - Decide by a session parameter
    - Temporal Validity
        - Add a valid-time dimension to rows
            - decide which data is non-operational 
            - Can be archived and hidden from normal queries
- SQL example
    - `CREATE TABLE employees (empno number(8), fullname varchar2(30)) ROW ARCHIVAL`
    - _Hidden_ Column `ORA_ARCHIVE_STATE` varchar2(4000) added implicitly
        - Value: 0=active, 1=inactive
        - Can be selected explicitly
        - Can be updated explicitly
        - `UPDATE employees SET ORA_ARCHIVE_STATE= DBMS_ILM.ARCHIVESTATENAME(1) WHERE ...`
        - `UPDATE employees SET ORA_ARCHIVE_STATE= DBMS_ILM.ARCHIVESTATENAME(0) WHERE ...`
    - By default only active (0) rows are shown in queries
        - `ALTER SESSION SET ROW ARCHIVAL VISIBILITY= ALL`
        - `ALTER SESSION SET ROW ARCHIVAL VISIBILITY= ACTIVE`
    - `ALTER TABLE employees NO ROW ARCHIVAL`
        - Hidden column `ORA_ARCHIVE_STATE` dropped
- **Not supported by Multitenant database**

### Differentiate between ILM and Valid-Time Temporal 
### Set and use Valid Time Temporal 

- Valid Time Temporal
    - Define Row validity by **start and end** date or timestamp (vs ORA_ARCHIVE_STATE)
    - Business relevance (hire date) can be easier to control
    - SQL example 1
        - `CREATE TABLE emp1 (empno number(8), fullname varchar2(30)， user_start date, user_end date) PERIOD FOR user_time(user_start, user_end)`
        - Column explicitly created: user_start and user_end
    - SQL example 2
        - `CREATE TABLE emp2 (empno number(8), fullname varchar2(30)) PERIOD FOR user_time`
        - Two hidden colimns implicitly created: **user_time_start** and **user_time_end**
    - Query data by
        - AS OF (!)
        - PERIOD FOR
            - `SELECT * FROM emp2 VERSIONS PERIOD FOR user_time BEWTEEN date'2011-01-01' AND date'2013-01-01'`
                - which is `user_time_start <= date'2011-01-01' AND user_time_end >= date'2013-01-01'`
        - DBMS_FLASHBACK_ARCHIVE
            - `exec DBMS_FLASHBACK_ARCHIVE.ENABLE_AT_VALID_TIME('ALL')`
                - Visibility at full level; Default
            - `exec DBMS_FLASHBACK_ARCHIVE.ENABLE_AT_VALID_TIME('CURRENT')`
                - Visibility at session current time
            - `exec DBMS_FLASHBACK_ARCHIVE.ENABLE_AT_VALID_TIME('ASOF', to_timestamp('10-NOV-13 08:45:01 a.m.'))`
                - As of specific timestamp
- **Not supported by Multitenant database**


## Other Enhancements [! Fit to where? !]
https://www.totalsem.com/0071819967dl/ Extra Info

### Database Migration Assistance for Unicode (DMU)
- New Tool to migrate databases from standard character sets to Unicode
    - Previous tool: CCSSCAN and CSALTER
    - New tool reduce downtime
    - Located at $ORACLE_HOME/dmu/dmu/bin

### Row limiting cluase and Secure File LOB Enhancements
- In 12c default, all LOB use SecureFile LOB
    - Init Para `DB_SECUREFILE`= PREFERRED when COMPATIBILE is 12.1.0.0.0 or higher
        - LOB are created as SecureFile unless BASICFILE specified in LOB storage clause
        - LOB will not inherit BASICFILE setting unless explicitly declared
        - Improve Performance in 12c
    - Init Para `DB_SECUREFILE`= PREMITTED when COMPATIBILE is 11.2.x.x.x
        - LOB are allowed to created as SecureFile but not required
- Row limit clause
    - Similar to Top-N query but having more semantics
        - But ROW LIMIT clause are **placed after** ORDER BY clause
    - OFFSET Nbr [ROW | ROWS] : Nbr of rows to skip, default 0
    - FETCH nbr ROW | nbr PERCENT [ ONLY | WITH TIES ]: Nbr of rows or percent to fetch
- Advanced Row Compression
    - Originally Advance Compression Option (ACO)
    - Originally all columns uncompressed on updated rows
    - Now only updated columns are uncompressed on updated rows
    - SQL `create table tab1 ... row store compress basic`
    - SQL `create table tab1 ... row store compress advanced`
    - Basic Table Compression is a part of 12c EE
    - Advanced Compression is a part of 12c Advanced Compression Option

### Configure Extended Data Types
- Max size of VARCHAR2 and NVARCHAR2 increased from 4000 bytes to 32767 bytes
    -  Requires: Init Para `MAX_STRING_SIZE`= EXTENDED
        - Run @ut132k.sql in _database upgrade mode_
        - Cannot Revert EXTENDED back to STANDARD (4000 bytes)
    - Extended String column are stored out-of-line
    - Normally do not extend String of **existing** column
        - Because existing String are stored inline
            - Row-chaining for long String
        - Re-create the table instead (CTAS)
        - Re-create indexes: Pre-existing index does not support extension of String
