# utl-using-a-magic-string-to-recover-from-a-frozen-sas-session
Using a magic string to recover from a frozen sas session  
    %let pgm=utl-using-a-magic-string-to-recover-from-a-frozen-sas-session;

    Using a magic string to recover from a frozen sas session

    Change in  Magic String

    The magic string is used to recover from a frozen SAS session

    * BEFORE SAS94M7 SAS WOULD FREEZE ON ME WITH SYNTAX ISSUES WITH THE OPEN CODE %IF
    * Less likely in SAS94M7?

    * Here is the case
    * Note the missing %end;

    * Note proc options is not run;

    %if ROGER = ROGER %then %put hello

    proc options;
    run;quit;

    How to fix only tested in SAS94M7

    I changed my magic string to handle some syntax issues with open code %if

    SAS 9.4M7

    Put this on function key 1

    ~%end;%mend;;;;;/*'*/ *);*};*];*/;/*"*/;run;quit;%end;end;run;endcomp;%utlfix;

    To recover from frozen SAS

    Hit function key 1

    This will appear on the editor

    %end;%mend;;;;;/*'*/ *);*};*];*/;/*"*/;run;quit;%end;end;run;endcomp;%utlfix;

    Highlite and submit the magic string

    Note ypu may need to run the highlited code mutiple times to recover

    %macro utlfix(dum);

    * fix frozen sas and restore to invocation ;
     dm "odsresults;clear;";
     ods results off;
     options ls=171 ps=65;run;quit;
     ods listing;
     ods select all;
     ods excel close;
     ods graphics off;
     proc printto;run;
     goptions reset=all;
     endsubmit;
     endrsubmit;
     run;quit;
     %utlopts;

    %mend utlfix;
