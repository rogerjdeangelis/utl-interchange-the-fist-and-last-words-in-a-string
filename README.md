# utl-interchange-the-fist-and-last-words-in-a-string
Interchange the fist and last words in a string 

    Interchange the fist and last words in a string                                                                                
                                                                                                                                   
      Given                                                                                                                        
         name=Smith John Mr.                                                                                                       
                                                                                                                                   
      Interchage first last                                                                                                        
         name=Mr. John Smith                                                                                                       
                                                                                                                                   
      Three Solutions                                                                                                              
                                                                                                                                   
         1. FCMP utl_pop (FCMP function on end)                                                                                    
         2. DOSUBL                                                                                                                 
         3. Tranwrd                                                                                                                
         3. R                                                                                                                      
            Jay-sf profile                                                                                                         
            https://stackoverflow.com/users/6574038/jay-sf                                                                         
                                                                                                                                   
    github                                                                                                                         
    https://tinyurl.com/y3ss6ns5                                                                                                   
    https://github.com/rogerjdeangelis/utl-interchange-the-fist-and-last-words-in-a-string                                         
                                                                                                                                   
    stackoverflow R                                                                                                                
    https://tinyurl.com/y5mpas4r                                                                                                   
    https://stackoverflow.com/questions/56824838/how-can-i-switch-the-positions-of-the-first-and-last-element-of-a-character-stri  
                                                                                                                                   
    *_                   _                                                                                                         
    (_)_ __  _ __  _   _| |_                                                                                                       
    | | '_ \| '_ \| | | | __|                                                                                                      
    | | | | | |_) | |_| | |_                                                                                                       
    |_|_| |_| .__/ \__,_|\__|                                                                                                      
            |_|                                                                                                                    
    ;                                                                                                                              
                                                                                                                                   
    data have;                                                                                                                     
      input name $32.;                                                                                                             
    cards4;                                                                                                                        
    Jones John Paul Mr.                                                                                                            
    Doe John Mr.                                                                                                                   
    ;;;;                                                                                                                           
    run;quit;                                                                                                                      
                                                                                                                                   
                                                                                                                                   
    WORK.HAVE total obs=2                                                                                                          
                                                                                                                                   
      NAME                                                                                                                         
                                                                                                                                   
      Jones John Paul Mr.                                                                                                          
      Doe John Mr.                                                                                                                 
                                                                                                                                   
    *            _               _                                                                                                 
      ___  _   _| |_ _ __  _   _| |_                                                                                               
     / _ \| | | | __| '_ \| | | | __|                                                                                              
    | (_) | |_| | |_| |_) | |_| | |_                                                                                               
     \___/ \__,_|\__| .__/ \__,_|\__|                                                                                              
                    |_|                                                                                                            
    ;                                                                                                                              
                                                                                                                                   
    Work WANT total obs=2                                                                                                          
                                                                                                                                   
      NAME                                                                                                                         
                                                                                                                                   
      Mr. John Paul Jones                                                                                                          
      Mr. John Doe                                                                                                                 
                                                                                                                                   
                                                                                                                                   
    *          _       _   _                                                                                                       
     ___  ___ | |_   _| |_(_) ___  _ __  ___                                                                                       
    / __|/ _ \| | | | | __| |/ _ \| '_ \/ __|                                                                                      
    \__ \ (_) | | |_| | |_| | (_) | | | \__ \                                                                                      
    |___/\___/|_|\__,_|\__|_|\___/|_| |_|___/                                                                                      
                                                                                                                                   
    ;                                                                                                                              
                                                                                                                                   
    *_       __                                                                                                                    
    / |     / _| ___ _ __ ___  _ __                                                                                                
    | |    | |_ / __| '_ ` _ \| '_ \                                                                                               
    | |_   |  _| (__| | | | | | |_) |                                                                                              
    |_(_)  |_|  \___|_| |_| |_| .__/                                                                                               
                              |_|                                                                                                  
    ;                                                                                                                              
                                                                                                                                   
    data want;                                                                                                                     
                                                                                                                                   
      length  word string $200;                                                                                                    
                                                                                                                                   
      set have;                                                                                                                    
                                                                                                                                   
      * pops a word off the list and returns the word and reduced string'                                                          
                                                                                                                                   
      call utl_pop(name,word,"first");  beg=word;                                                                                  
      call utl_pop(name,word,"last");                                                                                              
      name=catx(" ",word,name,beg);                                                                                                
                                                                                                                                   
      drop word string beg;                                                                                                        
                                                                                                                                   
    run;quit;                                                                                                                      
                                                                                                                                   
    *____           _                 _     _                                                                                      
    |___ \       __| | ___  ___ _   _| |__ | |                                                                                     
      __) |     / _` |/ _ \/ __| | | | '_ \| |                                                                                     
     / __/ _   | (_| | (_) \__ \ |_| | |_) | |                                                                                     
    |_____(_)   \__,_|\___/|___/\__,_|_.__/|_|                                                                                     
                                                                                                                                   
    ;                                                                                                                              
    * more flexible - any arrangement of words?                                                                                    
    %symdel args wrds / nowarn;                                                                                                    
    data want;                                                                                                                     
                                                                                                                                   
      set have;                                                                                                                    
                                                                                                                                   
      args=cats('"',tranwrd(strip(name)," ",'","'),'"');                                                                           
      wrds=countw(name);                                                                                                           
                                                                                                                                   
      call symputx("args",args);                                                                                                   
      call symputx("wrds",wrds);                                                                                                   
                                                                                                                                   
      rc=dosubl('                                                                                                                  
         data _null_;                                                                                                              
           array parts[&wrds] $24 (&args);                                                                                         
           select ;                                                                                                                
              when ( &wrds = 3) name=catx(" ",parts[&wrds],parts[2],parts[1]);                                                     
              when ( &wrds = 4) name=catx(" ",parts[&wrds],parts[2],parts[3],parts[1]);                                            
           end; * no otherwise fail if not 3 or 4;                                                                                 
           call symputx("xch",name);                                                                                               
         run;quit;                                                                                                                 
     ');                                                                                                                           
                                                                                                                                   
      name=symget("xch");                                                                                                          
                                                                                                                                   
      drop args wrds rc;                                                                                                           
                                                                                                                                   
    run;quit;                                                                                                                      
                                                                                                                                   
    *_____     _                                   _                                                                               
    |___ /    | |_ _ __ __ _ _ ____      ___ __ __| |                                                                              
      |_ \    | __| '__/ _` | '_ \ \ /\ / / '__/ _` |                                                                              
     ___) |   | |_| | | (_| | | | \ V  V /| | | (_| |                                                                              
    |____(_)   \__|_|  \__,_|_| |_|\_/\_/ |_|  \__,_|                                                                              
                                                                                                                                   
    ;                                                                                                                              
                                                                                                                                   
    * cannot have mutiple exact substrings;                                                                                        
    data want;                                                                                                                     
                                                                                                                                   
      length chop name $200;                                                                                                       
                                                                                                                                   
      set have;                                                                                                                    
                                                                                                                                   
       chop = tranwrd(strip(name),scan(name,1) ,"");                                                                               
       chop = tranwrd(strip(chop),scan(name,-1," "),"");                                                                           
       name=catx(" ",scan(name,-1),chop,scan(name,1));                                                                             
                                                                                                                                   
       keep name;                                                                                                                  
                                                                                                                                   
    run;quit;                                                                                                                      
                                                                                                                                   
    *_  _       ____                                                                                                               
    | || |     |  _ \                                                                                                              
    | || |_    | |_) |                                                                                                             
    |__   _|   |  _ <                                                                                                              
       |_|(_)  |_| \_\                                                                                                             
                                                                                                                                   
    ;                                                                                                                              
                                                                                                                                   
    %utl_submit_r64('                                                                                                              
    str1 <- "Doe John Mr.";                                                                                                        
    str2 <- "Jones John Paul Mr.";                                                                                                 
    Reduce(paste, el(strsplit(str1, " "))[3:1]);                                                                                   
    Reduce(paste, el(strsplit(str2, " "))[c(4, 2, 3, 1)]);                                                                         
    ');                                                                                                                            
                                                                                                                                   
    [1] "Mr. John Doe"                                                                                                             
    [1] "Mr. John Paul Jones"                                                                                                      
                                                                                                                                   
    * __                                      _                                                                                    
     / _| ___ _ __ ___  _ __     ___ ___   __| | ___                                                                               
    | |_ / __| '_ ` _ \| '_ \   / __/ _ \ / _` |/ _ \                                                                              
    |  _| (__| | | | | | |_) | | (_| (_) | (_| |  __/                                                                              
    |_|  \___|_| |_| |_| .__/   \___\___/ \__,_|\___|                                                                              
                       |_|                                                                                                         
    ;                                                                                                                              
                                                                                                                                   
                                                                                                                                   
    options cmplib=work.functions;                                                                                                 
    proc fcmp outlib=work.functions.temp;                                                                                          
    Subroutine utl_pop(string $,word $,action $);                                                                                  
        outargs word, string;                                                                                                      
        length word $4096;                                                                                                         
        select (upcase(action));                                                                                                   
          when ("LAST") do;                                                                                                        
            call scan(string,-1,_action,_length,' ');                                                                              
            word=substr(string,_action,_length);                                                                                   
            string=substr(string,1,_action-1);                                                                                     
          end;                                                                                                                     
                                                                                                                                   
          when ("FIRST") do;                                                                                                       
            call scan(string,1,_action,_length,' ');                                                                               
            word=substr(string,_action,_length);                                                                                   
            string=substr(string,_action + _length);                                                                               
          end;                                                                                                                     
                                                                                                                                   
          otherwise put "ERROR: Invalid action";                                                                                   
                                                                                                                                   
        end;                                                                                                                       
    endsub;                                                                                                                        
    run;quit;                                                                                                                      
                                                                                                                                   
                                                                                                             
