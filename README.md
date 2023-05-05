MODULE m3_JCup
    !****************************************
  ! VERSION   : v1.0
  !
  ! LANGUAGE  : ENGLISH
  !
  ! NAME      : CUP for JUST
  !
  ! PROJECT   : Titanium coatin for cup
  !
  ! HISTORY   : Created BF 2020.7.10
  !
  ! AUTHOR    : czy
  !
  !********************  ********************
  
  LOCAL VAR num nPlanetDiameter:=194;
  LOCAL PERS num nOffsX:=-69;
  LOCAL PERS num nOffsY:=0;
  LOCAL PERS num tag1:=0;
  LOCAL PERS num lPos:=1;
  LOCAL PERS robtarget sPos:=[[1107.23,-431.71,1565],[0.693086,0.187213,0.664883,-0.206191],[-1,-1,0,0],[0,0,0,0,0,0]];
  LOCAL PERS speeddata r2_Vspeed{8}:=[
   [100,500,50,50],[100,500,50,50],[100,500,50,50],
   [95,500,50,50],[95,500,50,50],[90,500,50,50],[90,500,50,50],[85,500,50,50]
 ];
 !CONST robtarget temp:=[[-163.85,16.03,255.80],[0.382677,0.000158702,0.923882,0.000213088],[-1,0,-1,0],[0,0,0,0,0,0]];
  LOCAL PERS speeddata r3_Vspeed:=[10,500,50,50];
  LOCAL PERS speeddata r3_90:=[90,500,5000,1000];
  LOCAL PERS speeddata r3_70:=[70,500,5000,1000];
  LOCAL PERS speeddata vlow:=[100,500,5000,1000];
  LOCAL PERS num cooltime:=360;
  LOCAL PERS num number{4}:=[0,0,0,0];
  LOCAL PERS string status{4}:=["prepare","prepare","prepare","prepare"];
  
  LOCAL PERS robtarget r3_cup_star{9}:=[
                                [[-85.8,0,195],[0.382683,0,0.92388,0],[0,0,-1,0],[0,0,0,0,0,0]],
                                [[-116.799,0,184.799],[0.382683,0,0.92388,0],[0,0,-1,0],[0,0,0,0,0,0]],
                                [[-118.449,0,182.998],[0.422618,0,0.906308,0],[0,0,-1,0],[0,0,0,0,0,0]],
                                [[-119.936,0,181.06],[0.461749,0,0.887011,0],[0,0,-1,0],[0,0,0,0,0,0]],
                                [[-121.249,0,179],[0.5,0,0.866025,0],[0,0,-1,0],[0,0,0,0,0,0]],
                                [[-122.377,0,176.833],[0.5373,0,0.843391,0],[0,0,-1,0],[0,0,0,0,0,0]],
                                [[-124.046,0,172.247],[0.608761,0,0.793353,0],[0,0,-1,0],[0,0,0,0,0,0]],
                                [[-124.893,0,167.44],[0.67559,0,0.737277,0],[0,0,-1,0],[0,0,0,0,0,0]],
                                [[-125,0,165],[0.707107,0,0.707107,0],[0,0,-1,0],[0,0,0,0,0,0]]
                                ];
                                
    CONST robtarget r2_cup_350{9}:=[
                                  [[-163.85,16.03,255.80],[0.382677,0.000158702,0.923882,0.000213088],[-1,0,-1,0],[0,0,0,0,0,0]],
                                  [[-174.756,11.497,260.632],[0.422702888,-3.9688E-05,0.906268319,-1.5933E-05],[-1,0,-1,0],[0,0,0,0,0,0]],
                                  [[-190.201,20.367,245.502],[0.500060317,4.8044E-05,0.865990575,3.6061E-05],[-1,0,-1,0],[0,0,0,0,0,0]],
                                  [[-195.236,12.213,240.65],[0.500025346,0.000166915,0.866010749,8.7085E-05],[-1,0,-1,0],[0,0,0,0,0,0]],
                                  [[-203.279,5.772,231.653],[0.53739845,9.2838E-05,0.843328464,-9.168E-06],[-1,0,-1,0],[0,0,0,0,0,0]],
                                  [[-210.607,6.5,217.242],[0.573645412,0.000203475,0.819103717,-3.6396E-05],[-1,0,-1,0],[0,0,0,0,0,0]],
                                  [[-218.123,11.39,200.389],[0.608821866,0.000170016,0.793306943,1.5876E-05],[-1,0,-1,0],[0,0,0,0,0,0]],
                                  [[-222.461,14.816,180.431],[0.642704486,0.000119371,0.766114174,4.656E-05],[-1,0,-1,0],[0,0,0,0,0,0]],
                                  [[-229.1,9.352,151.414],[0.685496682,0.000449564,0.728071802,0.002355536],[-1,0,-1,0],[0,0,0,0,0,0]]
                             ];
    CONST robtarget r2_cup_300{9}:=[
                              [[-136.341,10.973,225.442],[0.382722496,8.251E-06,0.92386335,4.2767E-05],[-1,0,-1,0],[0,0,0,0,0,0]],
                              [[-149.938,8.666,219.923],[0.422638242,-2.1001E-05,0.906298469,-1.3624E-05],[-1,0,-1,0],[0,0,0,0,0,0]],
                              [[-158.582,8.413,210.551],[0.500017996,7.7828E-05,0.866015009,4.6186E-05],[-1,0,-1,0],[0,0,0,0,0,0]],
                              [[-166.263,3.921,198.224],[0.499978773,0.000106273,0.866037653,3.184E-06],[-1,0,-1,0],[0,0,0,0,0,0]],
                              [[-172.023,7.749,186.766],[0.537309174,8.9578E-05,0.843385345,-6.4802E-05],[-1,0,-1,0],[0,0,0,0,0,0]],
                              [[-172.932,12.608,186.996],[0.573578008,8.234E-05,0.819150936,-6.9798E-05],[-1,0,-1,0],[0,0,0,0,0,0]],
                              [[-176.28,16.371,182.028],[0.608815367,6.5326E-05,0.793311946,-2.8288E-05],[-1,0,-1,0],[0,0,0,0,0,0]],
                              [[-179.27,9.952,168.962],[0.64272517,4.1803E-05,0.766096831,-1.5958E-05],[-1,0,-1,0],[0,0,0,0,0,0]],
                              [[-180.122,3.513,155.867],[0.685483037,0.000431007,0.728084503,0.002403327],[-1,0,-1,0],[0,0,0,0,0,0]]
                             ];
    LOCAL PERS robtarget pwork{9}:=[
                             [[-163.85,16.03,255.8],[0.382677,0.000158702,0.923882,0.000213088],[-1,0,-1,0],[0,0,0,0,0,0]],
                             [[-174.756,11.497,260.632],[0.422703,-3.9688E-05,0.906268,-1.5933E-05],[-1,0,-1,0],[0,0,0,0,0,0]],
                             [[-190.201,20.367,245.502],[0.50006,4.8044E-05,0.865991,3.6061E-05],[-1,0,-1,0],[0,0,0,0,0,0]],
                             [[-195.236,12.213,240.65],[0.500025,0.000166915,0.866011,8.7085E-05],[-1,0,-1,0],[0,0,0,0,0,0]],
                             [[-203.279,5.772,231.653],[0.537398,9.2838E-05,0.843328,-9.168E-06],[-1,0,-1,0],[0,0,0,0,0,0]],
                             [[-210.607,6.5,217.242],[0.573645,0.000203475,0.819104,-3.6396E-05],[-1,0,-1,0],[0,0,0,0,0,0]],
                             [[-218.123,11.39,200.389],[0.608822,0.000170016,0.793307,1.5876E-05],[-1,0,-1,0],[0,0,0,0,0,0]],
                             [[-222.461,14.816,180.431],[0.642704,0.000119371,0.766114,4.656E-05],[-1,0,-1,0],[0,0,0,0,0,0]],
                             [[-229.1,9.352,151.414],[0.685497,0.000449564,0.728072,0.00235554],[-1,0,-1,0],[0,0,0,0,0,0]]
                             ];
     LOCAL PERS speeddata v2_cup:=[3,10,100,100];
     
      LOCAL PERS robtarget cBorder:=[[-218.123,11.39,200.389],[0.608822,0.000170016,0.793307,1.5876E-05],[-1,0,-1,0],[0,0,0,0,0,0]];
     LOCAL PERS robtarget ts:=[[-159.45,23.14,450.77],[0.528798,0.00364895,0.848739,-0.00155993],[-1,0,-1,0],[-0.000596802,9E+09,9E+09,9E+09,9E+09,9E+09]];
     LOCAL PERS robtarget ts1:=[[-159.33,23.43,250.93],[0.528892,0.0036304,0.84868,-0.00153849],[-1,0,-1,0],[-0.000596802,9E+09,9E+09,9E+09,9E+09,9E+09]];
     LOCAL PERS speeddata vts:=[90,500,50,50];
    ! CONST robtarget pstar:=[[-159.01,25.96,274.46],[0.314487,-0.00746309,0.949219,0.00503333],[-1,0,-1,0],[0,0,0,0,0,0]];
     CONST robtarget p2:=[[-135.902,-9.929,237.076],[0.422536471,-4.41E-07,0.906345922,2.5178E-05],[-1,0,-1,0],[0,0,0,0,0,0]];
     CONST robtarget p3:=[[-144.493,-12.055,227.901],[0.461713824,-4.7338E-05,0.88702894,-4.4319E-05],[-1,0,-1,0],[0,0,0,0,0,0]];
     CONST robtarget p4:=[[-173.055,-29.168,173.432],[0.500005787,7.0499E-05,0.86602206,-1.0827E-05],[-1,-1,0,0],[0,0,0,0,0,0]];
     CONST robtarget p5:=[[-171.533,8.993,189.854],[0.53729421,7.7854E-05,0.843394877,-8.0823E-05],[-1,0,-1,0],[0,0,0,0,0,0]];
     CONST robtarget p6:=[[-171.17,-18.641,175.286],[0.573550215,1.8768E-05,0.819170403,-4.126E-05],[-1,-1,0,0],[0,0,0,0,0,0]];
     CONST robtarget p7:=[[-182.125,-15.376,166.23],[0.608795402,2.3081E-05,0.793327269,-3.3582E-05],[-1,-1,-1,0],[0,0,0,0,0,0]];
     CONST robtarget p8:=[[-185.385,-21.023,167.768],[0.642801693,5.8E-08,0.766032625,-2.3041E-05],[-1,-1,0,0],[0,0,0,0,0,0]];
     CONST robtarget p9:=[[-181.668,-11.3,152.045],[0.685479927,0.000339285,0.728087413,0.002423589],[-1,-1,0,0],[0,0,0,0,0,0]];
     CONST robtarget p1:=[[-141.95,-15.783,228.24],[0.382674897,-2.1949E-05,0.923883068,2.596E-06],[-1,-1,-1,0],[0,0,0,0,0,0]];
  PROC rProdukt3()
    !*************************************** 
    ! FUNKTION   : Parameterdefinition

    ! define the name of the product which will be displayed on the Robot User Panel
    stProdukt1234:="m3_Cup";
    ! Bewegungsablauefe definieren
    sRoutineHeating:="r3_border_Heating";
    sRoutineTiFine1:="r3_border";
    sRoutineTiCoarse1:="r3_cup";
    !sRoutineTiCoarse1:="r2_cup_Ti_z";
    sRoutineTiFine2:="";
    sRoutineTiCoarse2:="";
    sRoutineTiFine3:="";
    sRoutineTiCoarse3:="";
    sRoutineTiFine4:="";
    sRoutineTiCoarse4:="";
    sRoutineTiFine5:="";
    sRoutineHA:="";
    
    ! define the number of passages
    nPasHeating:=0;
    nPasTiFine1:=0;
    nPasTiCoarse1:=3;
    nPasTiFine2:=0;
    nPasTiCoarse2:=0;
    nPasTiFine3:=0;
    nPasTiCoarse3:=0;
    nPasTiFine4:=0;
    nPasTiCoarse4:=0;
    nPasTiFine5:=0;
    nPasHA:=0;
    ! define the minimum waiting time for the cooling of a part
    nMinCoolingTimePlanet:=2;
    ! Define the recipe for the corresponding coating step
    nRecipeHeating:=2;
    nRecipeTiFine1:=6;
    nRecipeTiCoarse1:=6; 
    nRecipeTiFine2:=3;
    nRecipeTiCoarse2:=4; 
    nRecipeTiFine3:=3;
    nRecipeTiCoarse3:=4; 
    nRecipeTiFine4:=3;
    nRecipeTiCoarse4:=4; 
    nRecipeTiFine5:=3;
    nRecipeHA:=3; 
    ! define if rotation of the planets should be used or not
    bRotation1234:=TRUE;
    !define the offsets for a tangential coating
    !nOffsX:=-Round(Sin(45)*(nPlanetDiameter/2));
    !nOffsY:=Round(Cos(45)*(nPlanetDiameter/2));
    sCtime;
    setStposition;
  ENDPROC
  
  PROC r3_Cup_Ti()
    VAR robtarget pTop;
    VAR robtarget pNext; 
    VAR speeddata r2_wobble:=[80,500,10,10];
    VAR speeddata r2_speed:=[3,10,100,100];
    ! For manual Testing of a single routine use the rTpInputParameter routine to select the
    ! coating Step/process and the Planet position you want to use
    If OpMode()<>OP_AUTO  rTpInputParameter;
    ! TCP definieren
    IF Heating() tAktuell:=TCP225;
    IF TiFine() tAktuell:=TCP250_12h;
    IF TiCoarse() tAktuell:=TCP250_3h9h;
    IF Hydoxylapatit() tAktuell:=TCP275_6h;
    ! Werkobjekt definieren
    IF nPos=1 wobjAktuell:=wobjpos1;
    IF nPos=2 wobjAktuell:=wobjpos2;
    IF nPos=3 wobjAktuell:=wobjpos3;
    IF nPos=4 wobjAktuell:=wobjpos4;
    IF nPos<3 THEN
      nYDirection:=-1;
    ELSE
      nYDirection:=1;
    ENDIF
    CONFL \Off;
    ! ********************  ******************** 
    pwork:=r2_cup_350;
    !IF npos=2 pwork:=r2_cup_350;
    pTop:=pwork{1};
    pNext:=pwork{2};
    movel ptop,v200,z5,tAktuell\WObj:=wobjAktuell;
    WaitTime 6;
    rPendelnDreieck pTop,pNext,nCupDiam/3,1.5,r2_wobble,z1;
    FOR i FROM 3 TO 9 step 1 DO
        movel pwork{i},r2_speed,z5,tAktuell\WObj:=wobjAktuell;
    ENDFOR
    FOR j FROM 8 TO 2 STEP -1 DO
        movel pwork{j},r2_speed,z5,tAktuell\WObj:=wobjAktuell;
    ENDFOR
    rPendelnDreieck pnext,ptop,nCupDiam/3,1.5,r2_wobble,z1;
    CONFL \On;
    RETURN;
  ENDPROC
  
  PROC r3_cup()
     rCooling;
     !SetDO doAblaufBeendet,0;
    If OpMode()<>OP_AUTO  rTpInputParameter;
    IF Heating() tAktuell:=TCP225;
    !IF TiFine() tAktuell:=TCP250_12h;
    IF TiFine() tAktuell:=TCP250_3h9h;
    IF TiCoarse() tAktuell:=TCP250_3h9h;
    IF Hydoxylapatit() tAktuell:=TCP275_6h;
    ! Werkobjekt definieren
    IF nPos=1 wobjAktuell:=wobjpos1;
    IF nPos=2 wobjAktuell:=wobjpos2;
    IF nPos=3 wobjAktuell:=wobjpos3;
    IF nPos=4 wobjAktuell:=wobjpos4;
    IF nPos<3 THEN
      nYDirection:=-1;
    ELSE
      nYDirection:=1;
    ENDIF
    CONFL \Off;
    pwork:=r2_cup_350;
   
    movel offs(pwork{1},7,0,10),v200,z5,tAktuell\WObj:=wobjAktuell;
    FOR t FROM 1 TO 6 DO
       movel offs(pwork{1},7,nYDirection*50,10),v60,z5,tAktuell\WObj:=wobjAktuell;
       movel offs(pwork{1},7,0,10),v60,z5,tAktuell\WObj:=wobjAktuell;
    ENDFOR

    movel pwork{1},v200,z5,tAktuell\WObj:=wobjAktuell;
    FOR i FROM 1 TO 8 STEP 1 DO
        movel pwork{i},r3_Vspeed,z5,tAktuell\WObj:=wobjAktuell;
        rPendelnDreieck pwork{i},pwork{i+1},40,5,r2_Vspeed{i},z1;
        !#################################
        IF i=7 THEN
           movel pwork{i},v100,z5,tAktuell\WObj:=wobjAktuell; 
           FOR t FROM 1 TO 7 DO
               movel offs(pwork{i},0,nYDirection*50,0),r3_70,z5,tAktuell\WObj:=wobjAktuell;
               movel pwork{i},v60,z5,tAktuell\WObj:=wobjAktuell;
           ENDFOR
        ENDIF
        !###############################
    ENDFOR
    FOR i FROM 9 TO 2 STEP -1 DO
        movel pwork{i},r3_Vspeed,z5,tAktuell\WObj:=wobjAktuell;
        rPendelnDreieck pwork{i},pwork{i-1},40,5,r2_Vspeed{i-1},z1;
        !##############
        IF i=7 THEN
           movel pwork{i},v100,z5,tAktuell\WObj:=wobjAktuell; 
           FOR p FROM 1 TO 7 DO
               movel offs(pwork{i},0,nYDirection*50,0),r3_70,z5,tAktuell\WObj:=wobjAktuell;
               movel pwork{i},v60,z5,tAktuell\WObj:=wobjAktuell;
           ENDFOR
        ENDIF
        !##################
    ENDFOR
    movel offs(pwork{1},7,0,10),r3_Vspeed,z5,tAktuell\WObj:=wobjAktuell;
    FOR t FROM 1 TO 6 DO
       movel offs(pwork{1},7,nYDirection*50,10),v60,z5,tAktuell\WObj:=wobjAktuell;
       movel offs(pwork{1},7,0,10),v60,z5,tAktuell\WObj:=wobjAktuell;
    ENDFOR
    CONFL \On;
  ENDPROC

  PROC sCtime()
        cooltime:=360;
        FOR i FROM 1 TO 4 DO
          IF  stTiCoarse1Cur{i} ="" cooltime:=cooltime+60;
        ENDFOR
  ENDPROC

PROC sStatus()
   status:=["","","",""];
   number:=[0,0,0,0];
ENDPROC  

  PROC setStposition()
   FOR i FROM 1 TO 4 DO
       IF stTiCoarse1Cur{i} <> "" THEN
           !sPos:="pAprPos"+Numtostr(i,0)+"_"+Numtostr(i,0);
           IF i=1 THEN 
               sPos:=pAprPos1_1 ;
               lPos:=1;
           ELSEIF i=2 THEN 
               sPos:=pAprPos2_1;
               lPos:=2;
           ELSEIF i=3 THEN
               sPos:=pAprPos3_1;
               lpos:=3;
           ELSEIF i=4 THEN 
               sPos:=pAprPos4_1;
               lPos:=4;
           ENDIF
           RETURN;
       ENDIF
   ENDFOR
  ENDPROC
  
  PROC rCooling()
    IF nPos=lpos AND nPasTiCoarse1Cur{lPos}>1 THEN
       MoveL pRecipeChange,v200,z5,TCP250\WObj:=wobj0;
       rStopPlanets;
       SetGO goRezept,1;
       WaitTime 1;
       SetDO doRezeptLesen,1;
       WaitTime 6;
       SetDO doRezeptLesen,0;
       TPErase;
       TPWrite "Current job : Cooling";
       TPWrite "Cooling Time : "+ NumToStr(cooltime/60,0)+"min";
       TPWrite "Cooling number : "+ NumToStr(nPasTiCoarse1Cur{lPos}-1,0);
       WaitTime cooltime;
       !WaitTime 10;
       rStartPlanetNormal;
       SetGO goRezept,nRecipeTiCoarse1;
       WaitTime 1;
       SetDO doRezeptLesen,1;
       TPErase;
       TPWrite "Change recipe......";
       WaitTime 6;
       SetDO doRezeptLesen,0;
       TPErase;
       tpreadfk tag1,"The cooling is over and spraying can be started","","","","","OK" ;
          IF tag1=5 THEN 
            MoveL sPos,v200,z5,TCP250\WObj:=wobj0;
            tag1:=0;
          ENDIF
    ENDIF
  ENDPROC
  PROC rsetCool()
   
  ENDPROC
  
  PROC r3_border_Heating()
    If OpMode()<>OP_AUTO  rTpInputParameter;
    IF Heating() tAktuell:=TCP225;
    !IF TiFine() tAktuell:=TCP250_12h;
    IF TiFine() tAktuell:=TCP250_3h9h;
    IF TiCoarse() tAktuell:=TCP250_3h9h;
    IF Hydoxylapatit() tAktuell:=TCP275_6h;
    ! Werkobjekt definieren
    IF nPos=1 wobjAktuell:=wobjpos1;
    IF nPos=2 wobjAktuell:=wobjpos2;
    IF nPos=3 wobjAktuell:=wobjpos3;
    IF nPos=4 wobjAktuell:=wobjpos4;
    IF nPos<3 THEN
      nYDirection:=-1;
    ELSE
      nYDirection:=1;
    ENDIF
    CONFL \Off;
     pwork:=r3_cup_star;
    movel pwork{1},v200,z5,tAktuell\WObj:=wobjAktuell;
        FOR i FROM 2 TO 9 STEP 1 DO
           movel pwork{i},v50,z5,tAktuell\WObj:=wobjAktuell;
        ENDFOR
        FOR i FROM 9 TO 1 STEP -1 DO
           movel pwork{i},v50,z5,tAktuell\WObj:=wobjAktuell;
        ENDFOR
    CONFL \On;
  ENDPROC
  
  PROC r3_border()
    If OpMode()<>OP_AUTO  rTpInputParameter;
    IF Heating() tAktuell:=TCP225;
    !IF TiFine() tAktuell:=TCP250_12h;
    IF TiFine() tAktuell:=TCP250_3h9h;
    IF TiCoarse() tAktuell:=TCP250_3h9h;
    IF Hydoxylapatit() tAktuell:=TCP275_6h;
    ! Werkobjekt definieren
    IF nPos=1 wobjAktuell:=wobjpos1;
    IF nPos=2 wobjAktuell:=wobjpos2;
    IF nPos=3 wobjAktuell:=wobjpos3;
    IF nPos=4 wobjAktuell:=wobjpos4;
    IF nPos<3 THEN
      nYDirection:=-1;
    ELSE
      nYDirection:=1;
    ENDIF
    CONFL \Off;
    cBorder:=r2_cup_350{7};
    movel cBorder,v200,z5,tAktuell\WObj:=wobjAktuell;
    FOR i FROM 1 TO 10 STEP 1 DO
        movel offs(cBorder,0,nYDirection*50,0),v60,z5,tAktuell\WObj:=wobjAktuell;
        movel cBorder,v60,z5,tAktuell\WObj:=wobjAktuell;
    ENDFOR
    CONFL \On;
  ENDPROC
  
  
  PROC r3_Low_heating()
     !rCooling;
     !SetDO doAblaufBeendet,0;
    If OpMode()<>OP_AUTO  rTpInputParameter;
    IF Heating() tAktuell:=TCP225;
    !IF TiFine() tAktuell:=TCP250_12h;
    IF TiFine() tAktuell:=TCP250_3h9h;
    IF TiCoarse() tAktuell:=TCP250_3h9h;
    IF Hydoxylapatit() tAktuell:=TCP275_6h;
    ! Werkobjekt definieren
    IF nPos=1 wobjAktuell:=wobjpos1;
    IF nPos=2 wobjAktuell:=wobjpos2;
    IF nPos=3 wobjAktuell:=wobjpos3;
    IF nPos=4 wobjAktuell:=wobjpos4;
    IF nPos<3 THEN
      nYDirection:=-1;
    ELSE
      nYDirection:=1;
    ENDIF
    CONFL \Off;
    pwork:=r3_cup_star;
    !movel pstar,v200,z5,tAktuell\WObj:=wobjAktuell;
    movel pwork{1},v200,z5,tAktuell\WObj:=wobjAktuell;
    !movel temp,v200,z5,tAktuell\WObj:=wobjAktuell;
    
    FOR t FROM 1 TO 2 DO
        IF t=1 THEN
            vlow:=v80;
        ELSE 
            vlow:=v100;
        ENDIF
        FOR i FROM 1 TO 8 STEP 1 DO
        movel pwork{i},r3_Vspeed,z5,tAktuell\WObj:=wobjAktuell;
        !rPendelnDreieck pwork{i},pwork{i+1},40,5,r2_Vspeed{i},z1;
        rPendelnDreieck pwork{i},pwork{i+1},40,5,vlow,z1;     !5.5
        !movel pwork{i+1},r3_Vspeed,z5,tAktuell\WObj:=wobjAktuell;
    ENDFOR
    FOR i FROM 9 TO 2 STEP -1 DO
        movel pwork{i},r3_Vspeed,z5,tAktuell\WObj:=wobjAktuell;
        !rPendelnDreieck pwork{i},pwork{i-1},40,5,r2_Vspeed{i-1},z1;
        rPendelnDreieck pwork{i},pwork{i-1},40,5,vlow,z1;      !5.5
        !movel pwork{i-1},r3_Vspeed,z5,tAktuell\WObj:=wobjAktuell;
    ENDFOR
    ENDFOR
    
    movel pwork{1},v100,z5,tAktuell\WObj:=wobjAktuell;
    CONFL \On;
  ENDPROC
  
ENDMODULE
