---
layout: post
title: IPython Notebook on SCC/GEO
permalink: ipynb_on_SCC
tags: [Python, SGE, SCC, BU]
summary: How to run IPython notebook on a SGE cluster
comments: true
---

Sketch:

+ Overview:
    * What is IPython notebook
    * Why is it so amazing?
    * http://www.nature.com/news/interactive-notebooks-sharing-the-code-1.16261
+ How to run on cluster (simple)
    * Module
    * Forwarding port
+ How to run on cluster (advanced)
    * Password protection
        - http://ipython.org/ipython-doc/1/interactive/public_server.html
    * Port forwarding to qsh session
        - Situation:
            + <local> --> <geo>: OKAY!
            + <local> --> <scc compute node>: NO
            + <local> --> <geo> --> <scc compute note>: OKAY!
        - http://superuser.com/questions/96489/ssh-tunnel-via-multiple-hops
        - http://superuser.com/questions/107679/forward-ssh-traffic-through-a-middle-machine
    * IPython profiles
    * IPython in parallel and cluster environment


