    %let pgm=utl-optimum-number-of-ten-cm-rods-to-cut-into-toy-trains-and-hot-wheels-axles-lp-linear-programming;

    %stop_submission;

    Optimum number of ten cm rods to cut into toy trains and hot wheels axles lp linear programming

    My Business gets orders for all kinds of axles for toys.
    The lengths, colors and diameters of the axles are different for each customer.

    My machine can only create 10 cm rods in various colors and diameters.
    I need to detremine the optimum number of 10cm rods to cut into axles for toys.
    I also need the optimum cuts of each rod to satisfy the customer specifications.

    Creating the rods is much mor expensive that cutting the rods, so I need an the
    optimum count of rods for each customer.

    Because of unique requirements from each customer I cannot reuse one customer wastes for another customer.

        Five Parts

             0 sas proc optmodel
               Rob Pratt <Rob.Pratt@SAS.COM>
             1 simple case
             2 moderate complexity
             3 complex solution
             4 macro solution
             5 r parmcards
             6 r submit macro

    github
    https://tinyurl.com/2s4ja2vd
    https://github.com/rogerjdeangelis/utl-optimum-number-of-ten-cm-rods-to-cut-into-toy-trains-and-hot-wheels-axles-lp-linear-programmi

    related repo
    github
    https://tinyurl.com/yhx4rxf7
    https://github.com/rogerjdeangelis/utl-minimize-cost-of-cattle-feed-with-nutritional-requirements-and-multiple-food-sources-lp-progr

    /*               _     _
     _ __  _ __ ___ | |__ | | ___ _ __ ___
    | `_ \| `__/ _ \| `_ \| |/ _ \ `_ ` _ \
    | |_) | | | (_) | |_) | |  __/ | | | | |
    | .__/|_|  \___/|_.__/|_|\___|_| |_| |_|
    |_|
    */
    /***************************************************************************************************************************/
    /*                                                                                                                         */
    /* The optimum number of rods I need to cut is the most critical number because of production costs                        */
    /* The number of cuts for each rod is less important. One company can order hundreds of axles.                             */
    /* Cannot use the waste from one cutomaer for another.                                                                     */
    /*                                                                                                                         */
    /*-------------------------------------------------------------------------------------------------------------------------*/
    /*                                     |                                       |                                           */
    /*  1 SIMPLE CASE (need 4 rods)        | 2 MODERATE COMPLEXITY (need 27 rods)  |     3 COMPLEX SOLUTION (need 94 rods)     */
    /*  ===========================        | ==================================--  |     =================================     */
    /*                                     |                                       |                                           */
    /*  Rods of length 10cm are in stock   | Rods of length 10cm are in stock      | We have rods of 5600cm in stock           */
    /*                                     |                                       |                                           */
    /*  We have the following orders       |  We have the following orders         | Orders from 13 companies                  */
    /*                                     |                                       |                                           */
    /*    Toys-R-Us: 5 axles length 2cm    |  Toys-R-Us 25 axles of length 3cm     | Orders                                    */
    /*    Walmart  : 2 axels lengtn 5cm    |  Walmart   20 axels of lengtn 5cm     |                                           */
    /*    Cosco    : 2 axles lengtn 10cm   |  Cosco     15 axles of lengtn 5cm     | Company     Axles Required Lengths        */
    /*                                     |  TOTAL     60 axles                   |                                           */
    /*                                     |                                       |                                           */
    /*  Total number of axles: 9           |                                       |  company01     22      1380cm             */
    /*                                     |  Optimal number stock pieces used: 27 |  company02     25      1520cm             */
    /*  Optimum cutting without any waste  |                                       |  company03     12      1560cm             */
    /*                                     |  Cutting patterns used:               |  company04     14      1710cm             */
    /*    Toys-R-Us Order                  |                                       |  company05     18      1820cm             */
    /*    ==============                   |               Rods    Cuts per Rod    |  company06     18      1880cm             */
    /*     5 axles length 2cm              |  Pattern 1 used  9      3 0 0         |  company07     20      1930cm             */
    /*                                     |  Pattern 2 used 10      0 2 0         |  company08     10      2000cm             */
    /*                     1               |  Pattern 3 used  8      0 0 2         |  company09     12      2050cm             */
    /*  |1 2|3 4|5 6|7 8|9 0| coror=red    |                                       |  company10     14      2100cm             */
    /*  |---|   |   |   |   | diameter=1cm |  Toys-R-Us Order: Cut 9 rods by 3cm   |  company11     16      2140cm             */
    /*  |   |---|   |   |   |              |            until 25 axles             |  company12     18      2150cm             */
    /*  |   |   |---|   |   | 1 rod        |                                       |  company13     20      2200cm             */
    /*  |   |   |   |---|   |              |  Walmart   Order: Cut 10 rods by 5cm  |  Axles Order  219                         */
    /*  |   |   |   |   |---| 5 axles      |            until 20 axless                                                        */
    /*                                     |                                       |  Optimal number of stock pieces used: 94  */
    /*      Walmart                        |  Cosco     Order: Cut 8 rods by 5cm   |                                           */
    /*      ======                         |            until 15 axless            |  Cutting patterns used:                   */
    /*   2 axles of length 5cm             |                                       |                                           */
    /*                                     |  Waste is melted down for new rods.   |           Rods       Cuts per Rod         */
    /*                     1               |                                       |  Pattern1   6 : 4 0 0 0 0 0 0 0 0 0 0 0 0 */
    /*  |1 2 3 4 5|6 7 8 9 0| color=blue   |                                       |  Pattern2   9 : 0 3 0 0 0 0 0 0 0 0 0 0 0 */
    /*  |         |         | diameter=2cm |                                       |  Pattern3   4 : 0 0 3 0 0 0 0 0 0 0 0 0 0 */
    /*  |         |         |              |                                       |  Pattern4   5 : 0 0 0 3 0 0 0 0 0 0 0 0 0 */
    /*  |         |         | 1 rod        |                                       |  Pattern5   6 : 0 0 0 0 3 0 0 0 0 0 0 0 0 */
    /*  |         |         |              |                                       |  Pattern6   9 : 0 0 0 0 0 2 0 0 0 0 0 0 0 */
    /*  |         |         | 2 axles      |                                       |  Pattern7  10 : 0 0 0 0 0 0 2 0 0 0 0 0 0 */
    /*                                     |                                       |  Pattern8   5 : 0 0 0 0 0 0 0 2 0 0 0 0 0 */
    /*        Cosco                        |                                       |  Pattern9   6 : 0 0 0 0 0 0 0 0 2 0 0 0 0 */
    /*       ======                        |                                       |  Pattern10  7 : 0 0 0 0 0 0 0 0 0 2 0 0 0 */
    /* 2 axles length 10cm(no cuts 2 rods) |                                       |  Pattern11  8 : 0 0 0 0 0 0 0 0 0 0 2 0 0 */
    /*                                     |                                       |  Pattern12  9 : 0 0 0 0 0 0 0 0 0 0 0 2 0 */
    /*                     1               |                                       |  Pattern13 10 : 0 0 0 0 0 0 0 0 0 0 0 0 2 */
    /*  |1 2 3 4 5 6 7 8 9 0| color=red    |                                       |  All Rods s94                             */
    /*  |                   |diameter=.5cm |                                       |                                           */
    /*  |                   |              |                                       |Interpretation                             */
    /*  |                   | 1 rod        |                                       |Pattern1: 4 cutsx1380cm on each of 6 rods  */
    /*  |                   | 1 axle       |                                       |                                           */
    /*  |                   |              |                                       |                                           */
    /*                                     |                                       | Waste is melted down for new rods.        */
    /*                                     |                                       |                                           */
    /*                     1               |                                       |                                           */
    /*  |1 2 3 4 5 6 7 8 9 0| color=red    |                                       |                                           */
    /*  |                   |diameter=.5cm |                                       |                                           */
    /*  |                   |              |                                       |                                           */
    /*  |                   | 1 rod        |                                       |                                           */
    /*  |                   | 1 axle       |                                       |                                           */
    /*  |                   |              |                                       |                                           */
    /*                                     |                                       |                                           */
    /*               Rods       Axles      |                                       |                                           */
    /*  Pattern 1 used 1 times: 5 0 0      |                                       |                                           */
    /*  Pattern 2 used 1 times: 0 2 0      |                                       |                                           */
    /*  Pattern 3 used 2 times: 0 0 1      |                                       |                                           */
    /*                                     |                                       |                                           */
    /*   No waste                          |                                       |                                           */
    /*                                     |                                       |                                           */
    /***************************************************************************************************************************/
    /*___                                                       _                       _      _
     / _ \   ___  __ _ ___   _ __  _ __ ___   ___    ___  _ __ | |_ _ __ ___   ___   __| | ___| |
    | | | | / __|/ _` / __| | `_ \| `__/ _ \ / __|  / _ \| `_ \| __| `_ ` _ \ / _ \ / _` |/ _ \ |
    | |_| | \__ \ (_| \__ \ | |_) | | | (_) | (__  | (_) | |_) | |_| | | | | | (_) | (_| |  __/ |
     \___/  |___/\__,_|___/ | .__/|_|  \___/ \___|  \___/| .__/ \__|_| |_| |_|\___/ \__,_|\___|_|
                            |_|                          |_|
    */

    /* simple */
    %let capacity = 10;
    data indata;
       input width demand;
       datalines;
     2 5
     5 2
    10 2
    ;

    /* moderate */
    %let capacity = 10;
    data indata;
       input width demand;
       datalines;
    3 25
    4 20
    5 15
    ;

    /* complex */
    %let capacity = 5600;
    data indata;
       input width demand;
       datalines;
    1380 22
    1520 25
    1560 12
    1710 14
    1820 18
    1880 18
    1930 20
    2000 10
    2050 12
    2100 14
    2140 16
    2150 18
    2200 20
    ;

    proc optmodel;
       /* declare parameters and sets */
       num capacity = &capacity;
       set ITEMS;
       num width  {ITEMS};
       num demand {ITEMS};
       num num_patterns init card(ITEMS);
       set PATTERNS = 1..num_patterns;
       num a {i in ITEMS, j in PATTERNS} = (if i = j then floor(capacity/width[i]) else 0);

       /* read input data */
       read data indata into ITEMS=[_N_] width demand;

       /* define optimization problem */
       var X {PATTERNS} >= 0 integer;
       min NumberOfRods = sum {j in PATTERNS} X[j];
       con DemandCon {i in ITEMS}:
          sum {j in PATTERNS} a[i,j] * X[j] >= demand[i];

       /* call solver */
       solve;

       /* clean up solution and save to output data set */
       for {j in PATTERNS} X[j] = round(X[j].sol);
       create data solution from [pattern]={j in PATTERNS: X[j] > 0} X {i in ITEMS} <col('i'||i)=a[i,j]>;
    quit;


    /*       _                 _
    / |  ___(_)_ __ ___  _ __ | | ___    ___ __ _ ___  ___
    | | / __| | `_ ` _ \| `_ \| |/ _ \  / __/ _` / __|/ _ \
    | | \__ \ | | | | | | |_) | |  __/ | (_| (_| \__ \  __/
    |_| |___/_|_| |_| |_| .__/|_|\___|  \___\__,_|___/\___|
                        |_|
    */

    %utl_rbeginx;
    parmcards4;
    library(lpSolve)

    # Define the problem

    # 1 simple case
    order_lengths <- c(2, 5, 10)
    order_quantities <- c(5, 2, 2)

    # Generate all possible cutting patterns
    generate_patterns <- function(stock_length, order_lengths) {
      patterns <- list()
      for (i in 1:length(order_lengths)) {
        pattern <- floor(stock_length / order_lengths[i])
        patterns[[i]] <- rep(0, length(order_lengths))
        patterns[[i]][i] <- pattern
      }
      return(do.call(rbind, patterns))
    }

    patterns <- generate_patterns(stock_length, order_lengths)
    patterns;

    # Set up the linear programming problem
    obj <- rep(1, nrow(patterns))  # Objective: minimize number of stock pieces used
    con <- t(patterns)  # Constraints: meet order quantities
    dir <- rep(">=", length(order_lengths))
    rhs <- order_quantities

    # Solve the problem
    solution <- lp("min", obj, con, dir, rhs, all.int = TRUE)
    str(solution)
    # Print results
    cat("Optimal number of stock pieces used:", solution$objval, "\n")
    cat("Cutting patterns used:\n")
    for (i in 1:length(solution$solution)) {
      if (solution$solution[i] > 0) {
        cat("Pattern", i, "used", solution$solution[i], "times:", patterns[i,], "\n")
      }
    }
    ;;;;
    %utl_rendx;

    /*           _               _
      ___  _   _| |_ _ __  _   _| |_
     / _ \| | | | __| `_ \| | | | __|
    | (_) | |_| | |_| |_) | |_| | |_
     \___/ \__,_|\__| .__/ \__,_|\__|
                    |_|
    */

     /**************************************************************************************************************************/
     /*                                                                                                                        */
     /*  Optimal number of stock pieces used: 4 rods - 9 axles                                                                 */
     /*  > cat("Cutting patterns used:\n")                                                                                     */
     /*  Cutting patterns used:                                                                                                */
     /*  > for (i in 1:length(solution$solution)) {                                                                            */
     /*  + if (solution$solution[i] > 0) {                                                                                     */
     /*  + cat("Pattern", i, "used", solution$solution[i], "times:", patterns[i,], "\n")                                       */
     /*  + }                                                                                                                   */
     /*  + }           rods      Cuts for Axles                                                                                */
     /*  Pattern 1 used 1 times: 5 0 0          Toys-R-Us                                                                      */
     /*  Pattern 2 used 1 times: 0 2 0          Walmart                                                                        */
     /*  Pattern 3 used 2 times: 0 0 1          Cosco                                                                          */
     /*  >              4                                                                                                      */
     /*                                                                                                                        */
     /**************************************************************************************************************************/

    /*___                        _                _                                   _           _ _
    |___ \   _ __ ___   ___   __| | ___ _ __ __ _| |_ ___    ___ ___  _ __ ___  _ __ | | _____  _(_) |_ _   _
      __) | | `_ ` _ \ / _ \ / _` |/ _ \ `__/ _` | __/ _ \  / __/ _ \| `_ ` _ \| `_ \| |/ _ \ \/ / | __| | | |
     / __/  | | | | | | (_) | (_| |  __/ | | (_| | ||  __/ | (_| (_) | | | | | | |_) | |  __/>  <| | |_| |_| |
    |_____| |_| |_| |_|\___/ \__,_|\___|_|  \__,_|\__\___|  \___\___/|_| |_| |_| .__/|_|\___/_/\_\_|\__|\__, |
                                                                               |_|                      |___/
    */

    %utl_rbeginx;
    parmcards4;
    library(lpSolve)

    # 1 simple case
    stock_length <- 10
    order_lengths <- c(3, 4, 5)
    order_quantities <- c(25, 20, 15)

    # Generate all possible cutting patterns
    generate_patterns <- function(stock_length, order_lengths) {
      patterns <- list()
      for (i in 1:length(order_lengths)) {
        pattern <- floor(stock_length / order_lengths[i])
        patterns[[i]] <- rep(0, length(order_lengths))
        patterns[[i]][i] <- pattern
      }
      return(do.call(rbind, patterns))
    }

    patterns <- generate_patterns(stock_length, order_lengths)
    patterns;

    # Set up the linear programming problem
    obj <- rep(1, nrow(patterns))  # Objective: minimize number of stock pieces used
    con <- t(patterns)  # Constraints: meet order quantities
    dir <- rep(">=", length(order_lengths))
    rhs <- order_quantities

    # Solve the problem
    solution <- lp("min", obj, con, dir, rhs, all.int = TRUE)
    str(solution)
    # Print results
    cat("Optimal number of stock pieces used:", solution$objval, "\n")
    cat("Cutting patterns used:\n")
    for (i in 1:length(solution$solution)) {
      if (solution$solution[i] > 0) {
        cat("Pattern", i, "used", solution$solution[i], "times:", patterns[i,], "\n")
      }
    }
    ;;;;
    %utl_rendx;

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /* Optimal number of stock pieces used: 27 - 60 axles                                                                     */
    /* > cat("Cutting patterns used:\n")                                                                                      */
    /* Cutting patterns used:                                                                                                 */
    /* > for (i in 1:length(solution$solution)) {                                                                             */
    /* + if (solution$solution[i] > 0) {                                                                                      */
    /* + cat("Pattern", i, "used", solution$solution[i], "times:", patterns[i,], "\n")                                        */
    /* + }                                                                                                                    */
    /* + }                             Axles                                                                                  */
    /* Pattern 1 used 9 times:  3 0 0   25                                                                                    */
    /* Pattern 2 used 10 times: 0 2 0   20                                                                                    */
    /* Pattern 3 used 8 times:  0 0 2   15                                                                                    */
    /*                                  60 axles                                                                              */
    /*                                                                                                                        */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*____                             _                       _       _   _
    |___ /    ___ ___  _ __ ___  _ __ | | _____  __  ___  ___ | |_   _| |_(_) ___  _ __
      |_ \   / __/ _ \| `_ ` _ \| `_ \| |/ _ \ \/ / / __|/ _ \| | | | | __| |/ _ \| `_ \
     ___) | | (_| (_) | | | | | | |_) | |  __/>  <  \__ \ (_) | | |_| | |_| | (_) | | | |
    |____/   \___\___/|_| |_| |_| .__/|_|\___/_/\_\ |___/\___/|_|\__,_|\__|_|\___/|_| |_|
                                |_|
    */

    %utl_rbeginx;
    parmcards4;
    library(lpSolve)

    # 3 complex solution
    stock_length<- 5600
    order_lengths<- c(1380, 1520, 1560, 1710, 1820, 1880, 1930, 2000, 2050, 2100, 2140, 2150, 2200)
    order_quantities<- c(22, 25, 12, 14, 18, 18, 20, 10, 12, 14, 16, 18, 20)

    # Generate all possible cutting patterns
    generate_patterns <- function(stock_length, order_lengths) {
      patterns <- list()
      for (i in 1:length(order_lengths)) {
        pattern <- floor(stock_length / order_lengths[i])
        patterns[[i]] <- rep(0, length(order_lengths))
        patterns[[i]][i] <- pattern
      }
      return(do.call(rbind, patterns))
    }

    patterns <- generate_patterns(stock_length, order_lengths)
    patterns;

    # Set up the linear programming problem
    obj <- rep(1, nrow(patterns))  # Objective: minimize number of stock pieces used
    con <- t(patterns)  # Constraints: meet order quantities
    dir <- rep(">=", length(order_lengths))
    rhs <- order_quantities

    # Solve the problem
    solution <- lp("min", obj, con, dir, rhs, all.int = TRUE)
    str(solution)
    # Print results
    cat("Optimal number of stock pieces used:", solution$objval, "\n")
    cat("Cutting patterns used:\n")
    for (i in 1:length(solution$solution)) {
      if (solution$solution[i] > 0) {
        cat("Pattern", i, "used", solution$solution[i], "times:", patterns[i,], "\n")
      }
    }
    ;;;;
    %utl_rendx;

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /*  Optimal number of stock pieces used: 94 (rods)                                                                        */
    /*                                                                                                                        */
    /*  > cat("Cutting patterns used:\n")                                                                                     */
    /*  Cutting patterns used:                                                                                                */
    /*  > for (i in 1:length(solution$solution)) {                                                                            */
    /*  + if (solution$solution[i] > 0) {                                                                                     */
    /*  + cat("Pattern", i, "used", solution$solution[i], "times:", patterns[i,], "\n")                                       */
    /*  + }                                                                                                                   */
    /*  + }                                                                                                                   */
    /*  Pattern1 used   6 times: 4 0 0 0 0 0 0 0 0 0 0 0 0                                                                    */
    /*  Pattern2 used   9 times: 0 3 0 0 0 0 0 0 0 0 0 0 0                                                                    */
    /*  Pattern3 used   4 times: 0 0 3 0 0 0 0 0 0 0 0 0 0                                                                    */
    /*  Pattern4 used   5 times: 0 0 0 3 0 0 0 0 0 0 0 0 0                                                                    */
    /*  Pattern5 used   6 times: 0 0 0 0 3 0 0 0 0 0 0 0 0                                                                    */
    /*  Pattern6 used   9 times: 0 0 0 0 0 2 0 0 0 0 0 0 0                                                                    */
    /*  Pattern7 used  10 times: 0 0 0 0 0 0 2 0 0 0 0 0 0                                                                    */
    /*  Pattern8 used   5 times: 0 0 0 0 0 0 0 2 0 0 0 0 0                                                                    */
    /*  Pattern9 used   6 times: 0 0 0 0 0 0 0 0 2 0 0 0 0                                                                    */
    /*  Pattern10 used  7 times: 0 0 0 0 0 0 0 0 0 2 0 0 0                                                                    */
    /*  Pattern11 used  8 times: 0 0 0 0 0 0 0 0 0 0 2 0 0                                                                    */
    /*  Pattern12 used  9 times: 0 0 0 0 0 0 0 0 0 0 0 2 0                                                                    */
    /*  Pattern13 used 10 times: 0 0 0 0 0 0 0 0 0 0 0 0 2                                                                    */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*  _                                                _       _   _
    | || |    _ __ ___   __ _  ___ _ __ ___    ___  ___ | |_   _| |_(_) ___  _ __
    | || |_  | `_ ` _ \ / _` |/ __| `__/ _ \  / __|/ _ \| | | | | __| |/ _ \| `_ \
    |__   _| | | | | | | (_| | (__| | | (_) | \__ \ (_) | | |_| | |_| | (_) | | | |
       |_|   |_| |_| |_|\__,_|\___|_|  \___/  |___/\___/|_|\__,_|\__|_|\___/|_| |_|

    */


    %macro cuts(
        stock_length    = 10
       ,order_lengths   = %str(2, 5, 10)
       ,order_quantities= %str(5, 2, 2)
       );

    %utl_submit_r64x("
    library(lpSolve);

    stock_length <- 10;
    order_lengths <- c(3, 4, 5);
    order_quantities <- c(25, 20, 15);

    stock_length     <- c(&stock_length) ;
    order_lengths    <- c(&order_lengths) ;
    order_quantities <- c(&order_quantities) ;

    generate_patterns <- function(stock_length, order_lengths) {
      patterns <- list();
      for (i in 1:length(order_lengths)) {
        pattern <- floor(stock_length / order_lengths[i]) ;
        patterns[[i]] <- rep(0, length(order_lengths));
        patterns[[i]][i] <- pattern ;
      };
      return(do.call(rbind, patterns));
    };

    patterns <- generate_patterns(stock_length, order_lengths);
    patterns;

    obj <- rep(1, nrow(patterns));
    con <- t(patterns);
    dir <- rep('>=', length(order_lengths));
    rhs <- order_quantities;

    solution <- lp('min', obj, con, dir, rhs, all.int = TRUE);
    str(solution);
    cat('Optimal number of stock pieces used:', solution$objval, '\n');
    cat('Cutting patterns used:\n');
    for (i in 1:length(solution$solution)) {
      if (solution$solution[i] > 0) {
        cat('Pattern', i, 'used', solution$solution[i], 'times:', patterns[i,], '\n');
      }
    };
    ");

    %mend cuts;

    %cuts;

    %cuts(
        stock_length    = 10
       ,order_lengths   = %str(3, 4, 5)
       ,order_quantities= %str(25, 20, 15)
       );

    %cuts(
        stock_length    = 5600
       ,order_lengths   = %str(1380, 1520, 1560, 1710, 1820, 1880, 1930, 2000, 2050, 2100, 2140, 2150, 2200)
       ,order_quantities= %str(22, 25, 12, 14, 18, 18, 20, 10, 12, 14, 16, 18, 20)
       );

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /* 1 SIMPLE CASE                                                                                                          */
    /* =============                                                                                                          */
    /*                                                                                                                        */
    /* Optimal number of stock pieces used: 4                                                                                 */
    /* Cutting patterns used:                                                                                                 */
    /* Pattern 1 used 1 times: 5 0 0                                                                                          */
    /* Pattern 2 used 1 times: 0 2 0                                                                                          */
    /* Pattern 3 used 2 times: 0 0 1                                                                                          */
    /*                                                                                                                        */
    /* 2 MODERATE COMPLEXITY                                                                                                  */
    /* =====================                                                                                                  */
    /*                                                                                                                        */
    /* Optimal number of stock pieces used: 27                                                                                */
    /* Cutting patterns used:                                                                                                 */
    /* Pattern 1 used 9 times: 3 0 0                                                                                          */
    /* Pattern 2 used 10 times: 0 2 0                                                                                         */
    /* Pattern 3 used 8 times: 0 0 2                                                                                          */
    /*                                                                                                                        */
    /* 3 COMPLEX SOLUTION                                                                                                     */
    /* ==================                                                                                                     */
    /*                                                                                                                        */
    /* Optimal number of stock pieces used: 94                                                                                */
    /* Cutting patterns used:                                                                                                 */
    /* Pattern 1 used 6 times: 4 0 0 0 0 0 0 0 0 0 0 0 0                                                                      */
    /* Pattern 2 used 9 times: 0 3 0 0 0 0 0 0 0 0 0 0 0                                                                      */
    /* Pattern 3 used 4 times: 0 0 3 0 0 0 0 0 0 0 0 0 0                                                                      */
    /* Pattern 4 used 5 times: 0 0 0 3 0 0 0 0 0 0 0 0 0                                                                      */
    /* Pattern 5 used 6 times: 0 0 0 0 3 0 0 0 0 0 0 0 0                                                                      */
    /* Pattern 6 used 9 times: 0 0 0 0 0 2 0 0 0 0 0 0 0                                                                      */
    /* Pattern 7 used 10 times: 0 0 0 0 0 0 2 0 0 0 0 0 0                                                                     */
    /* Pattern 8 used 5 times: 0 0 0 0 0 0 0 2 0 0 0 0 0                                                                      */
    /* Pattern 9 used 6 times: 0 0 0 0 0 0 0 0 2 0 0 0 0                                                                      */
    /* Pattern 10 used 7 times: 0 0 0 0 0 0 0 0 0 2 0 0 0                                                                     */
    /* Pattern 11 used 8 times: 0 0 0 0 0 0 0 0 0 0 2 0 0                                                                     */
    /* Pattern 12 used 9 times: 0 0 0 0 0 0 0 0 0 0 0 2 0                                                                     */
    /* Pattern 13 used 10 times: 0 0 0 0 0 0 0 0 0 0 0 0 2                                                                    */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*___                                                        _
    | ___|   _ __   _ __   __ _ _ __ _ __ ___   ___ __ _ _ __ __| |___   _ __ ___   __ _  ___ _ __ ___  ___
    |___ \  | `__| | `_ \ / _` | `__| `_ ` _ \ / __/ _` | `__/ _` / __| | `_ ` _ \ / _` |/ __| `__/ _ \/ __|
     ___) | | |    | |_) | (_| | |  | | | | | | (_| (_| | | | (_| \__ \ | | | | | | (_| | (__| | | (_) \__ \
    |____/  |_|    | .__/ \__,_|_|  |_| |_| |_|\___\__,_|_|  \__,_|___/ |_| |_| |_|\__,_|\___|_|  \___/|___/
                   |_|
    */

    /*----                                                                   ----*/
    /*---- note parmcards cannot be used inside a macro (use utl_submit_r64x ----*/
    /*----                                                                   ----*/

    %utlfkil(c:/temp/r_pgmx);
    %utlfkil(c:/temp/r_pgm);
    filename ft15f001 "c:/temp/r_pgm";
    %mend utl_rbeginx;

    %macro utl_rendx(return=)/des="utl_rbeginx uses parmcards and must end with utl_rendx macro";
    run;quit;
    * EXECUTE R PROGRAM;
    data _null_;
      infile "c:/temp/r_pgm";
      input;
      file "c:/temp/r_pgmx";
      lyn=resolve(_infile_);
      put lyn;
    run;quit;
    options noxwait noxsync;
    filename rut pipe "D:\r414\bin\r.exe --vanilla --quiet --no-save < c:/temp/r_pgmx";
    run;quit;
    data _null_;
      file print;
      infile rut;
      input;
      put _infile_;
      putlog _infile_;
    run;quit;
    data _null_;
      infile " c:/temp/r_pgm";
      input;
      putlog _infile_;
    run;quit;
    %if "&return" ne ""  %then %do;
      filename clp clipbrd ;
      data _null_;
       infile clp obs=1;
       input;
       putlog "xxxxxx  " _infile_;
       call symputx("&return.",_infile_,"G");
      run;quit;
      %end;
    filename ft15f001 clear;
    %mend utl_rendx;

    if you add this to r script and set return=fromr then
    sas macro variable fromr will be available to sas
    writeClipboard("roger");

    /*__                      _               _ _
     / /_    _ __   ___ _   _| |__  _ __ ___ (_) |_
    | `_ \  | `__| / __| | | | `_ \| `_ ` _ \| | __|
    | (_) | | |    \__ \ |_| | |_) | | | | | | | |_
     \___/  |_|    |___/\__,_|_.__/|_| |_| |_|_|\__|

    */

    %macro utl_submit_r64x(
          pgmx
         ,return=N
         ,resolve=N
         )/des="Semi colon separated set of R commands - drop down to R";
      %utlfkil(%sysfunc(pathname(work))/r_pgm.txt);
      /* clear clipboard */
      filename _clp clipbrd;
      data _null_;
        file _clp;
        put " ";
      run;quit;
      * write the program to a temporary file;
      filename r_pgm "%sysfunc(pathname(work))/r_pgm.txt" lrecl=32766 recfm=v;
      data _null_;
        length pgm $32756;
        file r_pgm;
        if substr(upcase("&resolve"),1,1)="Y" then do;
            pgm=resolve(&pgmx);
         end;
        else do;
            pgm=&pgmx;
         end;
         if index(pgm,"`") then pgm=tranwrd(pgm,"`","27"x);
        put pgm;
        /*putlog pgm;*/
      run;
      %let __loc=%sysfunc(pathname(r_pgm));
      * pipe file through R;
      filename rut pipe "D:\r414\bin\r.exe --vanilla --quiet --no-save < &__loc";
      data _null_;
        file print;
        infile rut recfm=v lrecl=32756;
        input;
        put _infile_;
        putlog _infile_;
      run;
      filename rut clear;
      filename r_pgm clear;
      * use the clipboard to create macro variable;
      %if %upcase(%substr(&return.,1,1)) ne N %then %do;
        filename clp clipbrd ;
        data _null_;
         infile clp;
         input;
         putlog "macro variable &return = " _infile_;
         call symputx("&return.",_infile_,"G");
        run;quit;
      %end;
    %mend utl_submit_r64x;

    /*              _
      ___ _ __   __| |
     / _ \ `_ \ / _` |
    |  __/ | | | (_| |
     \___|_| |_|\__,_|

    */

