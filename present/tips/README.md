tipoftheweek
============

Tips of the (hopefully) week for research for my group at BU

## Future ideas:

+ Source code versioning
    * Why do it - show example
        - Useful for you; perhaps even more useful for your users
    * General idea and diffs or patches
    * Current practices - SVN and Git
    * Git on cluster
+ dotfiles - bashrc and aliases
+ Reproducibility
    * http://ropensci.org/blog/2014/06/09/reproducibility/
    * http://theconversation.com/science-is-in-a-reproducibility-crisis-how-do-we-resolve-it-16998
    * http://spectrum.ieee.org/robotics/artificial-intelligence/machinelearning-maestro-michael-jordan-on-the-delusions-of-big-data-and-other-huge-engineering-efforts
    * How much of the wood is woody?
        - WOW! Full analysis, from dataset to PDF
        - http://richfitz.github.io/wood/
    * MRV... why reproduce the map if we can just perform accuracy assessment and get bias-corrected area estimate?
        - In-fighting in the literature about definitions of trees, changes, carbon densities, etc.
        - More knowledge of behind the scenes --> less pithy arguments?
        - Small samples means small disagreements can result in large differences in estimates
+ Remote utilities
    * nohup
    * screen
    * tmux
    * vnc
    * SSH-ing directly into SCC nodes:
        - http://superuser.com/questions/96489/ssh-tunnel-via-multiple-hops
        - http://superuser.com/questions/107679/forward-ssh-traffic-through-a-middle-machine
+ Workflow management
    * Needs:
        - orchestrate tasks
        - graphs
        - logging
        - SGE - qsub stuff
    * Libraries:
        - Ruffus
            - Python decorators to tie functions/etc together
        - pyutilib.workflow
        - Spotify's luigi (not usable on SGE?)
        - COSMOS
        - doit
+ 3rd party libraries
    * $H_0$: someone already wrote the thing you need
    * how to find it
    * how to search it
    * when is it not worth using
        - licensing
        - documentation
        - portability concerns
+ Benchmarks and profiles - how to speed up your code
    * CPU vs IO
    * Memory profiling
    * Bottlenecks and our cluster
        - Speed ~ # jobs
+ "Defensive programming"
    * User interfaces (command line)
    * Why check?
        - You can provide a clear message about what went wrong versus a stack trace
    * http://software-carpentry.org/v5/novice/python/05-defensive.html
+ Testing
    * Test driven development
        - Good when you know the expected behavior
    * Regression testing
        - Especially useful when iterating on your algorithm
    * **NOT** for exploratory; but for code you will reuse
    * http://science.gsfc.nasa.gov/sed/content/uploadFiles/highlight_files/TDD_For_Scientists.pdf
+ Databases
    * SQL language
    * In practice - sqlite
    * For geography - PostgreSQL with PostGIS
    * General knowledge - SQL vs noSQL / structured vs unstructured

## Resources

+ http://software-carpentry.org/lessons.html
