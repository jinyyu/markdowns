
        #include <algorithm>
        #include <random>
        #include <string>
        #include <vector>
        
        int main()
        {
          std::vector<std::string> vec;
          std::mt19937_64 gen(43);
        
          for (int count = 0; count < 3; ++count)
          {
            for (int i = 0; i < 10 * 1000 * 1000; ++i)
            {
              char buf[64];
              snprintf(buf, sizeof buf, "%016lx", gen());
              vec.push_back(buf);
            }
            std::sort(vec.begin(), vec.end());  // 如果用 tcmalloc 2.5，这行注释掉反而会变慢！
            vec.clear();
          }
        }



- Link your executable with -lprofiler
        
        g++ -std=c++11 -O2 -Wall -g -lprofiler main.cpp
        
- Run your executable with the CPUPROFILE environment var set:

       CPUPROFILE=/tmp/prof.out <path/to/binary> [binary args]
     
- Install gv
        
        sudo yum -y install gv graphviz
             
- Run pprof to analyze the CPU usage
        
       pprof <path/to/binary> /tmp/prof.out      # -pg-like text output
       pprof --gv <path/to/binary> /tmp/prof.out # really cool graphical output