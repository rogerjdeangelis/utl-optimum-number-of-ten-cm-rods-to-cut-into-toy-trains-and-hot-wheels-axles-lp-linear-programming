    %let pgm=utl-minimize-cost-of-cattle-feed-with-nutritional-requirements-and-multiple-food-sources-lp-program;

    Minimize cost of cattle feed with nutritional requirements using multiple food sources r linear programming

         TWO SOLUTIONS

              0 sas optmodel
                Rob Pratt <00000c5046759d08-dmarc-request@listserv.uga.edu>
              1 r no sas input
              2 r with sas input output

    github
    https://tinyurl.com/yhx4rxf7
    https://github.com/rogerjdeangelis/utl-minimize-cost-of-cattle-feed-with-nutritional-requirements-and-multiple-food-sources-lp-progr
                     _     _
     _ __  _ __ ___ | |__ | | ___ _ __ ___
    | `_ \| `__/ _ \| `_ \| |/ _ \ `_ ` _ \
    | |_) | | | (_) | |_) | |  __/ | | | | |
    | .__/|_|  \___/|_.__/|_|\___|_| |_| |_|
    |_|

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /*  The cost of corn, soybean and citrus change daily on the Chicago Merchantile Exchange.                                */
    /*                                                                                                                        */
    /*  Minimize the cost for a combination of corn, soybean and citrus using todays prices on the comodities market.         */
    /*  The mix must contain the right proportions of protein, fiber and energy(calories).                                    */
    /*                                                                                                                        */
    /*  The optimum minimum purchase price is $0.28 per pound for the following feed mix using 7/28/2024 commodity prices.    */
    /*  This mix has the correct proportions ofprotein, fiber and energy(calories), see below.                                */
    /*                                                                                                                        */
    /*    Buy  $0.08 of corn at      $0.30 per pound  0.27 pounds                                                             */
    /*    Buy  $0.04 of soybean at   $0.50 per pound  0.08 pounds                                                             */
    /*    Buy  $0.16 of citrus at    $0.20 per pound  0.80 pounds                                                             */
    /*                                                ===========                                                             */
    /*                                                1.15lb($0.28) mix with the right nutrient proportions                  */
    /*                                                                                                                        */
    /*    115 lbs of this feed mix would cost $28 (this mix has the right nutrient proportions)                               */
    /*                                                                                                                        */
    /*    The final equation                                                                                                  */
    /*                                                                                                                        */
    /*                corn       soybean    citrus                                                                            */
    /*                                                                                                                        */
    /*    min cost = .256*.30 + .0852*.50 + .796*.20  =  $0.28 per pound                                                      */
    /*                                                                                                                        */
    /*                $0.0768 +   $0.0426 +  $0.1592  =  $0.28                                                                */
    /*                                       =======                                                                          */
    /*                                       largest spend on citrus                                                          */
    /*                                       (low cost 0.20/lb and high in fiber and reasonable energy)                      */
    /*  Details                                                                                                               */
    /*  =======                                                                                                               */
    /*                                                                                                                        */
    /*  The cost of each food source on 7/28/2024 is                                                                          */
    /*                                                                                                                        */
    /*  corn    = $0.30 per pound                                                                                             */
    /*  soybean = $0.50 per pound                                                                                             */
    /*  citrus  = $0.20 per pound                                                                                             */
    /*                                                                                                                        */
    /*  I need to make sure the mix has these units of nutients                                                               */
    /*                                                                                                                        */
    /*  protein >= 18   units per lb                                                                                          */
    /*  fiber   <= 25   units per lb                                                                                          */
    /*  energy  >= 2500 units per lb                                                                                          */
    /*                                                                                                                        */
    /*  Nutient values for each food source                                                                                   */
    /*                                                                                                                        */
    /*                 food sources                                                                                           */
    /*             corn  soybean   citrus                                                                                     */
    /*                                                                                                                        */
    /*  cost(lb)  $0.30   $0.50     $0.20   per pound                                                                         */
    /*                                                                                                                        */
    /*  protein       9      44        15   units                                                                             */
    /*  fiber         2       7        30   units                                                                             */
    /*  energy     3400    2300      1800   units                                                                             */
    /*                                                                                                                        */
    /*                                                                                                                        */
    /*  SOLUTION                                                                                                              */
    /*               corn       soybean    citrus                                                                             */
    /*                                                                                                                        */
    /*  min cost = .256*.30 + .0852*.50 + .796*.20  =  $0.28 per pound                                                        */
    /*                                                                                                                        */
    /*              $0.0768 +   $0.0426 +  $0.1592  =  $0.28                                                                  */
    /*                                     =======                                                                            */
    /*                                     largest spend on citrus                                                            */
    /*                                      (low cost 0.20/lb and high in fiber and reasonable energy)                        */
    /*                                                                                                                        */
    /*  Lets check that we habe the right proportion of ingredients.                                                          */
    /*                                                                                                                        */
    /*    Corn        soybean      citrus                                                                                     */
    /*                                                                                                                        */
    /*   .256*9    + .0852*44   + .796*15    = 18     >= 18  protein                                                          */
    /*   .256*2    + .0852*7    + .796*30    = 25     <= 25  fiber                                                            */
    /*   .256*3500 + .085*2300  + .796*1800  = 2524   >= 2500 energy                                                          */
    /*                                                                                                                        */
    /*  They are met                                                                                                          */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*___                                _                       _      _
     / _ \   ___  __ _ ___    ___  _ __ | |_ _ __ ___   ___   __| | ___| |
    | | | | / __|/ _` / __|  / _ \| `_ \| __| `_ ` _ \ / _ \ / _` |/ _ \ |
    | |_| | \__ \ (_| \__ \ | (_) | |_) | |_| | | | | | (_) | (_| |  __/ |
     \___/  |___/\__,_|___/  \___/| .__/ \__|_| |_| |_|\___/ \__,_|\___|_|
     _                   _        |_|
    (_)_ __  _ __  _   _| |_
    | | `_ \| `_ \| | | | __|
    | | | | | |_) | |_| | |_
    |_|_| |_| .__/ \__,_|\__|
            |_|
    */


    data IngredientData;
       input ingredient $ protein fiber energy cost;
       datalines;
    Corn     9  2 3400 0.30
    Soybean 44  7 2300 0.50
    Hay     15 30 1800 0.20
    ;
    data RhsData;
       input constraint $ rhs;
       datalines;
    Protein   18
    Fiber     25
    Energy  2500
    ;
    /*
     _ __  _ __ ___   ___ ___  ___ ___
    | `_ \| `__/ _ \ / __/ _ \/ __/ __|
    | |_) | | | (_) | (_|  __/\__ \__ \
    | .__/|_|  \___/ \___\___||___/___/
    |_|
    */
    proc optmodel;
       set <str> INGREDIENTS;
       num protein {INGREDIENTS};
       num fiber {INGREDIENTS};
       num energy {INGREDIENTS};
       num cost {INGREDIENTS};
       read data IngredientData into INGREDIENTS=[ingredient] protein fiber energy cost;
       set <str> CONSTRAINTS;
       num rhs {CONSTRAINTS};
       read data RhsData into CONSTRAINTS=[constraint] rhs;
       var X {INGREDIENTS} >= 0;
       min Z = sum {i in INGREDIENTS} cost[i] * X[i];
       con ProteinCon:
          sum {i in INGREDIENTS} protein[i] * X[i] >= rhs['Protein'];
       con FiberCon:
          sum {i in INGREDIENTS} fiber[i] * X[i] <= rhs['Fiber'];
       con EnergyCon:
          sum {i in INGREDIENTS} energy[i] * X[i] >= rhs['Energy'];
       solve;
       print X;
    quit;
    /*           _               _
      ___  _   _| |_ _ __  _   _| |_
     / _ \| | | | __| `_ \| | | | __|
    | (_) | |_| | |_| |_) | |_| | |_
     \___/ \__,_|\__| .__/ \__,_|\__|
                    |_|
    */
    The SAS System
    The OPTMODEL Procedure
    Problem Summary
    Objective Sense                    Minimization
    Objective Function                 Z
    Objective Type                     Linear
    Number of Variables                3
    Bounded Above                      0
    Bounded Below                      3
    Bounded Below and Above            0
    Free                               0
    Fixed                              0
    Number of Constraints              3
    Linear LE (<=)                     1
    Linear EQ (=)                      0
    Linear GE (>=)                     2
    Linear Range0
    Constraint Coefficients            9

    The SAS System
    The OPTMODEL Procedure
    Solution Summary
    Solver                             LP
    AlgorithmDual                      Simplex
    Objective Function                 Z
    Solution Status                    Optimal
    Objective Value                    0.2786983588
    Primal Infeasibility               0
    Dual Infeasibility                 1.156482E-17
    Bound Infeasibility                0
    Iterations4
    Presolve Time                      0.00
    Solution Time                      0.00

    Solution

    Corn                               0.256027
    Hay                                0.796378
    Soybean                            0.085229


    /*                                        _                   _
    / |  _ __   _ __   ___    ___  __ _ ___  (_)_ __  _ __  _   _| |_
    | | | `__| | `_ \ / _ \  / __|/ _` / __| | | `_ \| `_ \| | | | __|
    | | | |    | | | | (_) | \__ \ (_| \__ \ | | | | | |_) | |_| | |_
    |_| |_|    |_| |_|\___/  |___/\__,_|___/ |_|_| |_| .__/ \__,_|\__|
                                                     |_|
    */

    %utl_rbeginx;
    parmcards4;
    library(lpSolve)

    # Define the cost vector
    cost <- c(0.30, 0.50, 0.20)

    # Define the constraint matrix
    # Each row represents a constraint (Protein, Fiber, Energy)
    # Each column represents an ingredient (Corn, Soybean, Hay)
    constraints <- matrix(c(9, 44, 15,           # Protein content
                            2, 7, 30,            # Fiber content
                            3400, 2300, 1800),   # Energy content
                          nrow = 3, byrow = TRUE)

    # Define the direction of the constraints
    # ">=" for Protein and Energy, "<=" for Fiber
    direction <- c(">=", "<=", ">=")

    # Define the right-hand side of the constraints
    rhs <- c(18, 25, 2500)

    # Solve the linear programming problem
    solution <- lp("min", cost, constraints, direction, rhs)

    # Print the solution
    solution$solution
    ;;;;
    %utl_rendx;

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /* > solution$solution                                                                                                    */
    /* [1] 0.2560272 0.0852292 0.7963780                                                                                      */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*___                    _ _   _                       _    __
    |___ \   _ __  __      _(_) |_| |__    ___  __ _ ___  (_)  / /__
      __) | | `__| \ \ /\ / / | __| `_ \  / __|/ _` / __| | | / / _ \
     / __/  | |     \ V  V /| | |_| | | | \__ \ (_| \__ \ | |/ / (_) |
    |_____| |_|      \_/\_/ |_|\__|_| |_| |___/\__,_|___/ |_/_/ \___/
     _                   _
    (_)_ __  _ __  _   _| |_
    | | `_ \| `_ \| | | | __|
    | | | | | |_) | |_| | |_
    |_|_| |_| .__/ \__,_|\__|
            |_|
    */

    %symdel
        cost
        direction
        rhs / nowarn;

    %let cost        = %str(0.30, 0.50, 0.20);
    %let direction   = %str(">=", "<=", ">=");
    %let rhs         = %str(18, 25, 2500);

    options validvarname=upcase;
    libname sd1 "d:/sd1";
    data sd1.have;
     input corn saybean citrus;
    cards4;
    9 44 15
    2 7 30
    3400 2300 1800
    ;;;;
    run;quit;

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /*   SD1.HAVE total obs=3                                                                                                 */
    /*                                                                                                                        */
    /*      CORN    SAYBEAN    CITRUS                                                                                         */
    /*                                                                                                                        */
    /*         9        44        15                                                                                          */
    /*         2         7        30                                                                                          */
    /*      3400      2300      1800                                                                                          */
    /*                                                                                                                        */
    /* %put &=cost     ;                                                                                                      */
    /* %put &=direction;                                                                                                      */
    /* %put &=rhs      ;                                                                                                      */
    /*                                                                                                                        */
    /* COST      = 0.30, 0.50, 0.20                                                                                           */
    /* DIRECTION = ">=", "<=", ">="                                                                                           */
    /* RHS       = 18, 25, 2500                                                                                               */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*
     _ __  _ __ ___   ___ ___  ___ ___
    | `_ \| `__/ _ \ / __/ _ \/ __/ __|
    | |_) | | | (_) | (_|  __/\__ \__ \
    | .__/|_|  \___/ \___\___||___/___/
    |_|
    */

    %utl_rbeginx;
    parmcards4;
    library(lpSolve)
    library(haven)
    constraints<-as.matrix(read_sas("d:/sd1/have.sas7bdat"))
    cost <- c(&cost)
    direction <- c(&direction)
    rhs <- c(&rhs)
    solution <- lp("min", cost, constraints, direction, rhs)
    solution$solution
    feed=as.character(as.vector(solution$solution))
    writeClipboard(paste(feed[1],feed[2],feed[3]))
    ;;;;
    %utl_rendx(return=feed);

    %put &=feed;

    %put Minimum cost %scan(&feed,1,%str( )) * CORN + %scan(&feed,2,%str( )) * SOYBEAN + %scan(&feed,2,%str( )) * CITRUS;


    data summarize;

      retain mincost
            protein
            protein_level
            fiber
            fiber_level
            energy
            energy_level
            ;

      array ns[3,3] n1-n9 (%utl_numary(sd1.have));
      array costs[3] corn soybean citrus (&cost);
      array contraints[3] $2 protein fiber energy (&direction);
      array coef[3] (&feed);

      mincost =coef[1] * corn  + coef[2]*soybean +  coef[3] * citrus;

       protein_level = coef[1] * ns[1,1]   + coef[2]*ns[1,2]  +  coef[3] * ns[1,3] ;
       fiber_level   = coef[1] * ns[2,1]   + coef[2]*ns[2,2]  +  coef[3] * ns[2,3] ;
       energy_level  = coef[1] * ns[3,1]   + coef[2]*ns[3,2]  +  coef[3] * ns[3,3] ;

       corn_cost= coef[1] * corn;
       soybean_cost= coef[2]*soybean;
       energy_cost= coef[3] * citrus;

       put  /
           'Mincost      '    @20   mincost                 //
           'Attained nutrient levels  ">=", "<=", ">=" are satisfied' /
           'Protein_level'    @20   protein_level           /
           'Fiber_level  '    @20   fiber_level             /
           'Energy_level '    @20   energy_level            //
           'Buys of Corn Soybean and Energy'                /
           'Corn_purchase  '  @20   corn_cost  dollar8.5    /
           'Soybean_purchase' @20   soybean_cost dollar8.5  /
           'Energy_purchase'  @20   energy_cost dollar8.5   //;
       put;

       keep mincost
            protein
            protein_level
            fiber
            fiber_level
            energy
            energy_level
            ;
    run;quit;

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /* FROM R                                                                                                                 */
    /* ======                                                                                                                 */
    /*                                                                                                                        */
    /* > solution$solution                                                                                                    */
    /* [1] 0.2560272 0.0852292 0.7963780                                                                                      */
    /*                                                                                                                        */
    /* BACK TO SAS                                                                                                            */
    /* ===========                                                                                                            */
    /*                                                                                                                        */
    /* %put &=feed;                                                                                                           */
    /*                                                                                                                        */
    /* FEED=0.256027164685908 0.0852292020373514 0.796378041878891                                                            */
    /*                                                                                                                        */
    /* Minimum cost = 0.256027164685908 * CORN + 0.0852292020373514 * SOYBEAN + 0.796378041878891 * CITRUS                    */
    /*                                                                                                                        */
    /* Mincost            0.2786983588                                                                                        */
    /*                                                                                                                        */
    /* Nutrient levels  ">=", "<=", ">=" are satisfied                                                                        */
    /* Protein_level      18                                                                                                  */
    /* Fiber_level        25                                                                                                  */
    /* Energy_level       2500                                                                                                */
    /*                                                                                                                        */
    /* Buys of Corn Soybean and Energy                                                                                        */
    /* Corn_purchase      $0.07681                                                                                            */
    /* Soybean_purchase   $0.04261                                                                                            */
    /* Energy_purchase    $0.15928                                                                                            */
    /*                    =========                                                                                           */
    /*                    $0.27869                                                                                            */
    /*                                                                                                                        */
    /**************************************************************************************************************************/


     /*              _
      ___ _ __   __| |
     / _ \ `_ \ / _` |
    |  __/ | | | (_| |
     \___|_| |_|\__,_|

    */

