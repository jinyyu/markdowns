    
        perf record -e cpu-clock -g -p 24366 
        perf script -i perf.data &> perf.unfold
        git clone https://github.com/brendangregg/FlameGraph
        ./stackcollapse-perf.pl perf.unfold &> perf.folded
        ./flamegraph.pl perf.folded > perf.svg
        
