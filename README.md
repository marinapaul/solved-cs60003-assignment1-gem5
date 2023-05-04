Download Link: https://assignmentchef.com/product/solved-cs60003-assignment1-gem5
<br>
gem5 is a system simulator that models CPUs at the microarchitecture level and all other associated structures such as caches, memory, interconnect buses, etc. It implements many architectural features that we have studied in this class. The purpose of this assignment is to help you get acquainted with gem5 and with the methodology for running simulations to estimate the performance of machines vis-`a-vis different benchmark programs.

gem5 allows the simulation of a wide range of CPUs, both functionally (correctness only) and for timing (correctness and efficiency). It supports multiple ISAs, including x86-64. <em>A tutorial session has already been provided on how to install and setup gem5</em>. The detailed slides are available on Moodle/ MS Teams. For more information on gem5, please visit <a href="http://learning.gem5.org/book/">http://learning.gem5.org/book/ </a>gem5 can simulate CPUs with different configurations (e.g. number of cores, pipeline complexity, cache size…) based on configuration scripts. How to write a sample configuration script has been shown in the tutorial (video available on course webpage). In this assignment, your task is to configure an Out-Of-Order CPU with a list of the microarchitectural parameters (provided below) that reflects the characteristic of a single-core x86 processor and run the provided benchmark program. More precisely, you will have to create different configuration combinations based on the parameters and their values mentioned in this document and run the provided benchmark program using those scripts. Then you will analyse the output statistics of each of these config combinations to select top 10 combinations and finally answer the questions mentioned in the later part of the document.

<h1>Procedure</h1>

<ol>

 <li>Follow the instructions discussed in the tutorial session to download, build and configure gem5. For your own understanding, run the benchmark program on your machine (outside gem5). You should also read through the source code because you will need to run the same benchmark from your custom config script.</li>

 <li>Configure your custom config script to reflect the following fixed parameters:

  <ul>

   <li>CPU model: Out-of-Order (DerivO3CPU)</li>

   <li>Caches: L1I, L1D, L2 (set associative)</li>

   <li>Clock Frequency: 2GHz</li>

   <li>Memory mode: timing</li>

   <li>Memory size: 1GB</li>

   <li>Memory controller: MemCtrl()</li>

   <li>DRAM type: DDR3 1600 8×8()</li>

   <li>NumberofReorderBuffer: 1</li>

   <li>l1 tag latency: 2</li>

   <li>l1 data latency: 2</li>

   <li>l1 response latency: 2</li>

   <li>l1 mshrs: 4</li>

   <li>l1 tgts per mshr: 20</li>

   <li>l2 tag latency: 20</li>

  </ul></li>

</ol>




<ul>

 <li>l2 data latency: 20</li>

 <li>l2 response latency: 20</li>

 <li>l2 mshrs: 20</li>

 <li>l2 tgts per mshr: 12</li>

 <li>cacheline: 64</li>

</ul>

<ol start="3">

 <li>The following parameters have multiple values. You are required to include all the parameters and test your script with each value of the parameters. For example, if there are <em>m </em>parameters, each having <em>n </em>values, you have to run <em>n<sup>m </sup></em>different configurations to cover all possible combinations. The variable parameters are listed below:

  <ul>

   <li>l1d size: 32kB, 64kB</li>

   <li>l1i size: 32kB, 64kB</li>

   <li>l2 size: 128kB, 256kB, 512kB</li>

   <li>l1 assoc: 2, 4, 8</li>

   <li>l2 assoc: 4, 8</li>

   <li>bp type: TournamentBP, BiModeBP, LocalBP</li>

   <li>LQEntries: 16, 32, 64</li>

   <li>SQEntries: 16, 32, 64</li>

   <li>ROBEntries: 128, 192</li>

   <li>numIQEntries: 16, 32, 64</li>

  </ul></li>

 <li>Run simulations of the benchmark program using your custom script by changing the values of the parameters mentioned in Point 3. You can also use gem5/configs/example/se.py and gem5/config/common/options.py with some modifications.</li>

 <li>Answer the following questions in a PDF document.

  <ul>

   <li>Analyze the m5out/stats.txt to extract different statistics for each of the config combinations.

    <ul>

     <li>Based on the CPI values, which are the top 10 configurations for the benchmark program?</li>

     <li>Why do you think these combinations of parameters works best for the given benchmark program? You might need to analyse the program source code in order to justify your claims.</li>

     <li>Provide a graph or plot for each of the top 10 combinations depicting the following <strong>– </strong>Cycles Per Instruction (CPI).

      <ul>

       <li>Mispredicted branches detected during execution.</li>

       <li>Number of branches that were predicted not taken incorrectly.</li>

       <li>Number of branches that were predicted taken incorrectly.</li>

       <li>Instructions Per Cycle (IPC).</li>

       <li>Number of BTB hit percentage.</li>

       <li>Number of overall miss cycles, miss rate, average overall miss latency.</li>

       <li>The number of ROB accesses (read and write both).</li>

       <li>Number of times the LSQ has become full, causing a stall.</li>

       <li>Number of loads that had data forwarded from stores.</li>

       <li>Number of times access to memory failed due to the cache being blocked.</li>

      </ul></li>

    </ul></li>

  </ul></li>

</ol>