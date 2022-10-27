# RegexPatterns
### SAS Logs

        internal static string rxNote { get { return @"NOTE:[\d\D]+?$"; } }
        internal static string RxDataStep { get { return @"NOTE:\sThere\swere\s(\d+)\sobservations\sread\sfrom\sthe\sdata\sset\s([\w_.]+)[\d\D]+?" + @"(?<DataStep>)NOTE:\sData\sstatement\sused[\d\D]+?(?=^([^\s]|$))"; } }

        //REPLACED ON AUG 6, 2015
        //internal static string RxProc { get { return @"NOTE:\sThere\swere\s(\d+)\sobservations\sread\sfrom\sthe\sdata\sset\s([\w_.]+)[\d\D]+?" + @"(?<Proc>)NOTE:\sProcedure\s([\w_]+)\sused[\d\D]+?(?=^([^\s]|$))"; } }
        internal static string RxProc { get { return @"(?<Proc>)NOTE:\sProcedure\s([\w_]+)\sused[\d\D]+?(?=^([^\s]|$))"; } }
        internal static string RxLibref { get { return @"(?<Libref>)NOTE:\sLibref\s[\w_]+\swas[\d\D]+?(?=^([^\s]|$))"; } }
        internal static string RxInitialization { get { return @"(?<Initialization>)NOTE:\sSAS\sinitialization\sused:[\d\D]+?(?=^([^\s]|$))"; } }
        internal static string RxFinalization { get { return @"(?<Finalization>)NOTE:\s+The\sSAS\sSystem\sUsed:[\d\D]+?(?=^\s*$)"; } }
        internal static string RxProcSql { get { return @"proc\s+sql[\d\D]+?quit\s*;"; } }

        //Data Step / Proc
        internal static string rxInputDataSet { get { return @"(?<Input>)NOTE:\sThere\swere\s(\d+)\sobservations\sread\sfrom\sthe\sdata\sset\s([\w_.]+)"; } }
        internal static string rxOutputDataSet { get { return @"(?<Output>)NOTE:\sThe\sdata\sset\s([\w_.]+)\shas\s(\d+)\sobservations\sand\s(\d+)\svariables"; } }

        //Lines
        internal static string rxProcedureLine { get { return @"NOTE:\sPROCEDURE\s([\w]+)\sused[\w\s()]+:"; } }

        //Libref
        internal static string rxLevels { get { return @"(?<Levels>)Levels:\s+([\w]+)"; } }      
        internal static string rxEngine { get { return @"(?<Engine>)Engine(\(\d\))?:\s+([\w]+)"; } }
        internal static string rxPhysicalFile { get { return @"(?<Physical>)Physical\sName(\(\d\))?:\s+(.+)"; } }

        //Errors/Warnings
        internal static string rxError { get { return @"^ERROR:\s([\d\D]+?)(?=\r)"; } }
        internal static string rxWarning { get { return @"^WARNING:\s([\d\D]+?)(?=\r)"; } }

        //Macros
        internal static string rxMPrintLogic { get { return @"(MPRINT|MLOGIC)\(([\w\.]+)\):\s+([\d\D]+?)$"; } }
        internal static string rxSpds { get { return @"(SPDS_NOTE):()\s([\d\D]+?)$"; } }
        internal static string rxMlogicStart { get { return @"^MLOGIC\([\w+\.]+\):\s+Beginning\sexecution.\s*$"; } }
        internal static string rxMlogicFinish { get { return @"^MLOGIC\([\w+\.]+\):\s+Ending\sexecution.\s*$"; } }

        //Other
        internal static string rxWhereClause { get { return @"\s+WHERE\s([\d\D]+?)(?=\r)"; } }
        internal static string rxLogTimestampedFileName { get { return @"([\w]+)_(\d{4}\.\d{2}\.\d{2}_\d{2}\.\d{2}\.\d{2})\.log"; } }

        //System Times
        internal static string rxRealTime { get { return @"\s*real\stime\s+:?\s*((\d+:)?(\d+:)?\d+\.\d+)\s(seconds)?"; } }
        internal static string rxUserCpuTime { get { return @"\s+user\scpu\stime\s+:?\s*((\d+:)?(\d+:)?\d+\.\d+)\s(seconds)?"; } }
        //Use a non-capturing group (?:) to look for the word system but ignore it as a match
        internal static string rxCpuTime { get { return @"^\s{2,}(?:system)?cpu\stime\s+:?\s*((\d+:)?(\d+:)?\d+\.\d+)\s(seconds)?"; } }

        internal static string rxLogStart { get { return @"[\d]+\s+The\sSAS\sSystem\s+([\d\:]+)[\w\s]+,\s([\w\d\s\,]+)$"; } }
        internal static string rxLogFinish { get { return @"[\d]+\s+The\sSAS\sSystem\s+([\d\:]+)[\w\s]+,\s([\w\d\s\,]+)$"; } }

        internal static string rxLogStartDetailed { get { return @"NOTE:\s+Log\s+file\s+opened\s+at\s+[\w\,]+\s([\d]+\s[\w]+\s+[\d]+)\s+([\d\:\.]+)"; } }
        internal static string rxLogFinishDetailed { get { return @"NOTE:\s+Log\s+file\s+opened\s+at\s+[\w\,]+\s([\d]+\s[\w]+\s+[\d]+)\s+([\d\:\.]+)"; } }

        //System Metrics
        internal static string rxMemory { get { return @"(?<=^\s+)memory\s+:?\s*(\d+)([kmgt])(?=\s*$)"; } }
        internal static string rxPageFaults { get { return @"(?<=^\s+)page\sfaults\s+:?\s*(\d+)(?=\s*$)"; } }
        internal static string rxPageReclaims { get { return @"(?<=^\s+)page\sreclaims\s+:?\s*(\d+)(?=\s*$)"; } }
        internal static string rxPageSwaps { get { return @"(?<=^\s+)page\sswaps\s+:?\s*(\d+)(?=\s*$)"; } }
        internal static string rxVoluntaryContextSwitches { get { return @"(?<=^\s+)voluntary\scontext\sswitches\s+:?\s*(\d+)(?=\s*$)"; } }
        internal static string rxInvoluntaryContextSwitches { get { return @"(?<=^\s+)involuntary\scontext\sswitches\s+:?\s*(\d+)(?=\s*$)"; } }
        internal static string rxBlockInputOperations { get { return @"(?<=^\s+)block\sinput\soperations\s+:?\s*(\d+)(?=\s*$)"; } }
        internal static string rxBlockOutputOperations { get { return @"(?<=^\s+)block\soutput\soperations\s+:?\s*(\d+)(?=\s*$)"; } }

        //Possible Errors
        internal static string rxErrorDataSetCopy { get { return @"([\d\D]+?:)?\s+data\s+[\d\D]+?;([\d\D]+?:)?\s+set\s+[\d\D]+?;([\d\D]+?:)?\s+run\s*;"; } }
        internal static string rxErrorCompression
        {
            get
            {
                return
                    @"NOTE:\s+Compressing\sdata\sset\s([\w\.]+)\sincreased\ssize\sby\s([\d\.]+)[\d\D]+?" +
                    @"Compressed\sis\s([\d]+)\spages;\sun-compressed\swould\srequire\s([\d]+)";
            }
        }
        internal static string rxErrorSqlPassThrough { get { return @"^SAS_SQL:[\d\D]+?(?>^\s*$)"; } }
