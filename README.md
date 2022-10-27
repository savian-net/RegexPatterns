# RegexPatterns
### SAS Logs

| Name                       | Group             | Pattern                                                                                                                                                     |
|----------------------------|-------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Note                       | General           | NOTE:[\d\D]+?$                                                                                                                                              |
| DataStep                   | General           | NOTE:\sThere\swere\s(\d+)\sobservations\sread\sfrom\sthe\sdata\sset\s([\w_.]+)[\d\D]+?" + @"(?<DataStep>)NOTE:\sData\sstatement\sused[\d\D]+?(?=^([^\s]|$)) |
| Proc                       | General           | (?<Proc>)NOTE:\sProcedure\s([\w_]+)\sused[\d\D]+?(?=^([^\s]|$))                                                                                             |
| Libref                     | General           | (?<Libref>)NOTE:\sLibref\s[\w_]+\swas[\d\D]+?(?=^([^\s]|$))                                                                                                 |
| Initialization             | General           | (?<Initialization>)NOTE:\sSAS\sinitialization\sused:[\d\D]+?(?=^([^\s]|$))                                                                                  |
| Finalization               | General           | (?<Finalization>)NOTE:\s+The\sSAS\sSystem\sUsed:[\d\D]+?(?=^\s*$)                                                                                           |
| ProcSql                    | General           | proc\s+sql[\d\D]+?quit\s*;                                                                                                                                  |
| InputDataSet               | Data Step - Proc  | (?<Input>)NOTE:\sThere\swere\s(\d+)\sobservations\sread\sfrom\sthe\sdata\sset\s([\w_.]+)                                                                    |
| OutputDataSet              | Data Step - Proc  | (?<Output>)NOTE:\sThe\sdata\sset\s([\w_.]+)\shas\s(\d+)\sobservations\sand\s(\d+)\svariables                                                                |
| ProcedureLine              | Data Step - Proc  | NOTE:\sPROCEDURE\s([\w]+)\sused[\w\s()]+:                                                                                                                   |
| WhereClause                | Data Step - Proc  | \s+WHERE\s([\d\D]+?)(?=\r)                                                                                                                                  |
| Levels                     | Libref            | (?<Levels>)Levels:\s+([\w]+)                                                                                                                                |
| Engine                     | Libref            | (?<Engine>)Engine(\(\d\))?:\s+([\w]+)                                                                                                                       |
| PhysicalFile               | Libref            | (?<Physical>)Physical\sName(\(\d\))?:\s+(.+)                                                                                                                |
| Error                      | Errors - Warnings | ^ERROR:\s([\d\D]+?)(?=\r)                                                                                                                                   |
| Warning                    | Errors - Warnings | ^WARNING:\s([\d\D]+?)(?=\r)                                                                                                                                 |
| MPrintLogic                | Macros            | (MPRINT|MLOGIC)\(([\w\.]+)\):\s+([\d\D]+?)$                                                                                                                 |
| Spds                       | Macros            | (SPDS_NOTE):()\s([\d\D]+?)$                                                                                                                                 |
| MlogicStart                | Macros            | ^MLOGIC\([\w+\.]+\):\s+Beginning\sexecution.\s*$                                                                                                            |
| MlogicFinish               | Macros            | ^MLOGIC\([\w+\.]+\):\s+Ending\sexecution.\s*$                                                                                                               |
| RealTime                   | System Times      | \s*real\stime\s+:?\s*((\d+:)?(\d+:)?\d+\.\d+)\s(seconds)?                                                                                                   |
| UserCpuTime                | System Times      | \s+user\scpu\stime\s+:?\s*((\d+:)?(\d+:)?\d+\.\d+)\s(seconds)?                                                                                              |
| CpuTime                    | System Times      | ^\s{2,}(?:system)?cpu\stime\s+:?\s*((\d+:)?(\d+:)?\d+\.\d+)\s(seconds)?                                                                                     |
| LogStart                   | System Times      | [\d]+\s+The\sSAS\sSystem\s+([\d\:]+)[\w\s]+,\s([\w\d\s\,]+)$                                                                                                |
| LogFinish                  | System Times      | [\d]+\s+The\sSAS\sSystem\s+([\d\:]+)[\w\s]+,\s([\w\d\s\,]+)$                                                                                                |
| LogStartDetailed           | System Times      | NOTE:\s+Log\s+file\s+opened\s+at\s+[\w\,]+\s([\d]+\s[\w]+\s+[\d]+)\s+([\d\:\.]+)                                                                            |
| LogFinishDetailed          | System Times      | NOTE:\s+Log\s+file\s+opened\s+at\s+[\w\,]+\s([\d]+\s[\w]+\s+[\d]+)\s+([\d\:\.]+)                                                                            |
| LogTimestampedFileName     | System Times      | ([\w]+)_(\d{4}\.\d{2}\.\d{2}_\d{2}\.\d{2}\.\d{2})\.log                                                                                                      |
| Memory                     | System Metrics    | (?<=^\s+)memory\s+:?\s*(\d+)([kmgt])(?=\s*$)                                                                                                                |
| PageFaults                 | System Metrics    | (?<=^\s+)page\sfaults\s+:?\s*(\d+)(?=\s*$)                                                                                                                  |
| PageReclaims               | System Metrics    | (?<=^\s+)page\sreclaims\s+:?\s*(\d+)(?=\s*$)                                                                                                                |
| PageSwaps                  | System Metrics    | (?<=^\s+)page\sswaps\s+:?\s*(\d+)(?=\s*$)                                                                                                                   |
| VoluntaryContextSwitches   | System Metrics    | (?<=^\s+)voluntary\scontext\sswitches\s+:?\s*(\d+)(?=\s*$)                                                                                                  |
| InvoluntaryContextSwitches | System Metrics    | (?<=^\s+)involuntary\scontext\sswitches\s+:?\s*(\d+)(?=\s*$)                                                                                                |
| BlockInputOperations       | System Metrics    | (?<=^\s+)block\sinput\soperations\s+:?\s*(\d+)(?=\s*$)                                                                                                      |
| BlockOutputOperations      | System Metrics    | (?<=^\s+)block\soutput\soperations\s+:?\s*(\d+)(?=\s*$)                                                                                                     |
| ErrorDataSetCopy           | ErrorsAsNotes     | ([\d\D]+?:)?\s+data\s+[\d\D]+?;([\d\D]+?:)?\s+set\s+[\d\D]+?;([\d\D]+?:)?\s+run\s*;                                                                         |
| ErrorCompression           | ErrorsAsNotes     | NOTE:\s+Compressing\sdata\sset\s([\w\.]+)\sincreased\ssize\sby\s([\d\.]+)[\d\D]+?Compressed\sis\s([\d]+)\spages;\sun-compressed\swould\srequire\s([\d]+)    |
| ErrorSqlPassThrough        | ErrorsAsNotes     | ^SAS_SQL:[\d\D]+?(?>^\s*$)                                                                                                                                  |
