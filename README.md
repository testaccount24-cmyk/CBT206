# CBT206
Converted to GitHub via [cbt2git](https://github.com/wizardofzos/cbt2git)

This is still a work in progress. GitHub repos will be deleted and created during this period...

```
//***FILE 206 IS FROM LINNEA NICHOLS OF THE FAIRFAX COUNTY          *   FILE 206
//*           GOVERNMENT IN FAIRFAX, VIRGINIA.  THIS FILE CONTAINS  *   FILE 206
//*           HER COLLECTION OF MOSTLY REXX ROUTINES TO HELP DASD   *   FILE 206
//*           STORAGE ADMINISTRATORS IN VARIOUS WAYS.  THE AIM OF   *   FILE 206
//*           THIS COLLECTION IS TO USE DCOLLECT DATA TO FIND OUT   *   FILE 206
//*           AND FORMAT ALL KINDS OF USEFUL INFORMATION.           *   FILE 206
//*                                                                 *   FILE 206
//*   - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -   *   FILE 206
//*                                                                 *   FILE 206
//*                   DCOLLECT REXX ROUTINES                        *   FILE 206
//*                                                                 *   FILE 206
//*        LINNEA NICHOLS                                           *   FILE 206
//*        FAIRFAX COUNTY GOVERNMENT                                *   FILE 206
//*        12000 GOVERNMENT CENTER PKWY                             *   FILE 206
//*        FAIRFAX, VA 22035                                        *   FILE 206
//*        703/324-2708                                             *   FILE 206
//*                                                                 *   FILE 206
//*        email:   lnicho@co.fairfax.va.us                         *   FILE 206
//*                                                                 *   FILE 206
//*        THIS FILE CONTAINS THE FOLLOWING MEMBERS:                *   FILE 206
//*                                                                 *   FILE 206
//*        $$PCDOC       YOU ARE READING IT                         *   FILE 206
//*                                                                 *   FILE 206
//*        REXXRTN       CONTAINS ALL REXX PROGRAMS.  NEEDS TO BE   *   FILE 206
//*                      UPLOADED TO A PS FILE (LRECL=80) AND THEN  *   FILE 206
//*                      UNLOADED TO A PDS USING IEBUPDTE.  SAMPLE  *   FILE 206
//*                      JCL TO UNLOAD IS IN $UPDJCL.  YOU WILL     *   FILE 206
//*                      NEED TO ALLOCATE A DSORG=PS, LRECL=80,     *   FILE 206
//*                      RECFM=FB FILE ON MVS TO UPLOAD REXXRTN     *   FILE 206
//*                      TO.  THEN RUN THE REXUPD JOB, BEING SURE   *   FILE 206
//*                      TO PUT IN YOUR OWN SYSIN AND SYSUT2 DATA   *   FILE 206
//*                      SET NAMES.  THE BEGINNING OF EACH PROGRAM  *   FILE 206
//*                      INCLUDES THE FOLLOWING: PURPOSE OF THE     *   FILE 206
//*                      REXX PROGRAM, INPUT FILES NEEDED, OUTPUT   *   FILE 206
//*                      FILES CREATED, AND PRESORT REQUIREMENTS.   *   FILE 206
//*                                                                 *   FILE 206
//*        PARSRTN       CONTAINS ROUTINES THAT CAN BE USED TO      *   FILE 206
//*                      PARSE RECORD TYPES D, M, C, V, T, AND B    *   FILE 206
//*                      AS WELL AS THE STANDARD HEADER.  NEEDS TO  *   FILE 206
//*                      BE UPLOADED TO A PS (LRECL=80) FILE AND    *   FILE 206
//*                      THEN UNLOADED TO A PDS USING IEBUPDTE.     *   FILE 206
//*                      SAMPLE JCL TO UNLOAD IT IS IN $UPDJCL.     *   FILE 206
//*                      USE THE SAME PROCEDURE AS DOCUMENTED FOR   *   FILE 206
//*                      REXXRTN.                                   *   FILE 206
//*                                                                 *   FILE 206
//*        $UPDJCL       SAMPLE JCL TO CREATE A PDS FROM THE PS     *   FILE 206
//*                      FILE YOU UPLOADED.                         *   FILE 206
//*                                                                 *   FILE 206
//*        DCOLJCL       SAMPLE JCL TO RUN DCOLLECT COLLECTION,     *   FILE 206
//*                      AND CREATE MOST OF THE FILES USED FOR      *   FILE 206
//*                      INPUT INTO THE REXX PROGRAMS.              *   FILE 206
//*                                                                 *   FILE 206
//*        IF YOU NEED HELP, HAVE SUGGESTIONS, OR JUST WANT         *   FILE 206
//*        TO TALK ABOUT DCOLLECT, PLEASE FEEL FREE TO CALL         *   FILE 206
//*        ME AT 703/324-2708 OR CONTACT ME VIA IBMMAIL AT          *   FILE 206
//*        US5RNFRN OR VIA INTERNET AT US5RNFRN@IBMMAIL.COM         *   FILE 206
//*                                                                 *   FILE 206
//*   THE ROUTINES INCLUDED ARE AS FOLLOWS:                         *   FILE 206
//*                                                                 *   FILE 206
//*     DASDVOLS                                                    *   FILE 206
//*         PURPOSE: READS TYPE V AND C RECORDS FOR VOLUME          *   FILE 206
//*                  DETAIL REPORT AND STORAGE GROUP SUMMARY        *   FILE 206
//*                  REPORT, READS TYPE T RECORDS FOR DFHSM         *   FILE 206
//*                  TAPE SUMMARY REPORT.                           *   FILE 206
//*                                                                 *   FILE 206
//*     DATERFSM                                                    *   FILE 206
//*         PURPOSE: READS TYPE D AND M RECORDS AND                 *   FILE 206
//*                  PRODUCES REPORTS OF DAYS FROM LAST             *   FILE 206
//*                  REFERENCE FOR THE FOLLOWING:                   *   FILE 206
//*                                                                 *   FILE 206
//*                     L0, ML1 AND ML2 DATA COMBINED               *   FILE 206
//*                     ALL L0 DATA                                 *   FILE 206
//*                     L0 SMS ONLY                                 *   FILE 206
//*                     L0 NONSMS ONLY                              *   FILE 206
//*                                                                 *   FILE 206
//*                  A DETAIL REPORT IS PRODUCED THAT LISTS         *   FILE 206
//*                  OUT ALL DSNS OLDER THAN 30 DAYS, NOT           *   FILE 206
//*                  INCLUDING VSAM INDEXES, VTOCS, VVDS,           *   FILE 206
//*                  PAGE AND TEMPORARY DSNS.                       *   FILE 206
//*                                                                 *   FILE 206
//*     DB2                                                         *   FILE 206
//*         PURPOSE: READS TYPE D RECORDS AND LISTS OUT ALL DB2     *   FILE 206
//*                  DSNS, INCLUDING VOLSER, CREATION DATE AND      *   FILE 206
//*                  ALLOCATED KBYTES.  TOTALS ALLOCATED KBYTES.    *   FILE 206
//*                                                                 *   FILE 206
//*     DCOLDREC                                                    *   FILE 206
//*         PURPOSE: PRINTS OUT DETAIL INFORMATION FOR EVERY        *   FILE 206
//*                  "D" AND "M" RECORD INPUT.                      *   FILE 206
//*                                                                 *   FILE 206
//*     DSORG                                                       *   FILE 206
//*         PURPOSE: BREAKOUT OF DATA SETS BY DSORG.  DONE BY       *   FILE 206
//*                  DSN COUNT AND BY KBYTES WITH PERCENTAGES.      *   FILE 206
//*                                                                 *   FILE 206
//*     ERRORS                                                      *   FILE 206
//*         PURPOSE: LISTS EVERY D RECORD THAT HAS ERROR BITS       *   FILE 206
//*                  SET.                                           *   FILE 206
//*                                                                 *   FILE 206
//*     EXPDT                                                       *   FILE 206
//*         PURPOSE: READS TYPE D AND M RECORDS FOR ALL DSNS        *   FILE 206
//*                  THAT HAVE AN EXPDT > 0.  (VSAM IS EXCLUDED     *   FILE 206
//*                  SINCE IT ALWAYS HAS AN EXPDT = 1999365).       *   FILE 206
//*                                                                 *   FILE 206
//*     HLQSUM                                                      *   FILE 206
//*         PURPOSE: READS DCOLLECT "D" "M" AND "B" RECORDS         *   FILE 206
//*                  AND PRODUCES A REPORT SUMMARIZED BY HLQ        *   FILE 206
//*                  OF BYTES ALLOCATED AT EACH LEVEL (L0,          *   FILE 206
//*                  ML1, AND ML2) AS WELL AS BACKUP BYTES.         *   FILE 206
//*                                                                 *   FILE 206
//*                  PRODUCES A SUMMARY REPORT OF THE FOLLOWING:    *   FILE 206
//*                                                                 *   FILE 206
//*                     TOTAL FROM VOLUME (V) RECORDS:              *   FILE 206
//*                        TOTAL AVAILABLE KBYTES                   *   FILE 206
//*                        TOTAL ALLOCATED KBYTES                   *   FILE 206
//*                        SMS AVAILABLE KBYTES                     *   FILE 206
//*                        SMS ALLOCATED KBYTES                     *   FILE 206
//*                                                                 *   FILE 206
//*                     TOTAL FROM D, M AND B RECORDS:              *   FILE 206
//*                        L0+ML1+ML2 DSN COUNT                     *   FILE 206
//*                        TOTAL L0 + ML1 + ML2 ALLOCATED           *   FILE 206
//*                        TOTAL BACKUP KBYTES                      *   FILE 206
//*                        L0 DSN COUNT                             *   FILE 206
//*                        L0 ALLOCATED KBYTES                      *   FILE 206
//*                        L0 USED KBYTES                           *   FILE 206
//*                        SMS DSN COUNT                            *   FILE 206
//*                        SMS ALLOCATED KBYTES                     *   FILE 206
//*                        ML1 DSN COUNT                            *   FILE 206
//*                        ML1 ALLOCATED KBYTES                     *   FILE 206
//*                        ML1 ORIGINAL KBYTES                      *   FILE 206
//*                        ML2 DSN COUNT                            *   FILE 206
//*                        ML2 ALLOCATED KBYTES                     *   FILE 206
//*                        ML2 ORIGINAL KBYTES                      *   FILE 206
//*                                                                 *   FILE 206
//*     MULTIVOL                                                    *   FILE 206
//*         PURPOSE: READS TYPE D RECORDS AND LISTS OUT             *   FILE 206
//*                  THE VOLSER AND DSN FOR ALL RECORDS             *   FILE 206
//*                  THAT HAVE A VOLUME SEQUENCE NUMBER > 1.        *   FILE 206
//*                                                                 *   FILE 206
//*     NONSMS                                                      *   FILE 206
//*         PURPOSE: READS TYPE D RECORDS AND LISTS OUT NON-SMS     *   FILE 206
//*                  DSNS AND THE VOLSER THEY ARE ON.  FOR EACH     *   FILE 206
//*                  HLQ, LISTS OUT NUMBER OF DATASETS, SIZE IN     *   FILE 206
//*                  KBYTES, SIZE FOR PRIME POOL (OURS IS           *   FILE 206
//*                  DEFINED AS <102400 KBYTES), SIZE FOR LARGE     *   FILE 206
//*                  POOL (ANY DSN >1024000 KBYTES), AND KBYTES     *   FILE 206
//*                  NOT REFERENCED IN THE LAST 30 DAYS.            *   FILE 206
//*                                                                 *   FILE 206
```
