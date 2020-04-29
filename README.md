# HVcMO

Hill-Valley-Clustering-based Variable Mesh Optimization (HVcMO) is an instance of VMO-N, the multimodal optimization framework for the VMO metaheuristic. All of them are described in:

Navarro R. and Kim C.H., "Niching Multimodal Landscapes Faster Yet Effectively: VMO and HillVallEA Benefit Together", Mathematics, vol. 8, 665, 2020. https://doi.org/10.3390/math8050665

# HillVallEA

At the same time, HVcMO is an extension of HillVallEA, detailed in:

Maree S.C., Alderliesten T., Thierens D., and Bosman, P.A.N., "Benchmarking HillVallEA for the GECCO 2019 Competition on Multimodal Optimization", arXiv preprint, arXiv:1907.10988, 2019.

Maree S.C., Alderliesten T., Thierens D., and Bosman, P.A.N., "Real-Valued Evolutionary Multi-Modal Optimization driven by Hill-Valley Clustering", In Proceedings of the Genetic and Evolutionary Computation Conference (GECCO 2018), Kyoto, Japan, pp. 857–864, 2018. https://doi.org/10.1145/3205455.3205477

# How does HVcMO modifies HillVallEA?

The main augmentations concern:

1- The application of the search operators of VMO over the truncated population (this is the biggest change).

2- The shrinkage of the size of the population to sample when the remaining budget is not enough to deal with a new population with the current size. This choice was indeed considered by S.C. Maree for HillVallEA, although discarded.

3- The alteration of the condition to increment the size parameters. In HillVallEA, that happens if no new peak is detected. Here, it occurs if also the population size was never reduced (this is a consequence of the 2nd modification).

4- The inclusion of other solutions in the 'rejection set', in particular, each master that represents a recently discovered peak, and the best elite found thus far.
    
# Compatibility of the source codes for HVcMO20a and for HillVallEA19

As evolutionary algorithms, HVcMO and HillVallEA share several conceptualizations, regardless of the names given, e.g. node (in VMO) means a solution and the mesh represents the population. In addition, there is a common reasoning behind any EA, implying that there are lots of common procedures. Then, instead of writing a totally new source code for HVcMO20a, it largely reutilizes the source code of HillVallEA19, the ultimate version of HillVallEA, also as an attempt to assure a fair comparability between their performances. The program for HillVallEA19 is available online under GNU General Public License v3.0:

By S.C. Maree at 
https://github.com/SCMaree/HillVallEA

# How to run HVcMO20a?

1- Clone the HillVallEA19 project from the repository told above.

2- Add the files "hvcmo20a.h" and "hvcmo20a.cpp" (provided here) to the HillVallEA package project inside your cloned HillVallEA-master.

3- Specify:

	class hvcmo_t;

	typedef std::shared_ptr<hvcmo_t> hvcmo_pt;

in the definitions for the namespace hillvallea, on the "hillvallea_internal.hpp" file in the HillVallEA project.

4- For a start, take the example script provided by S.C. Maree as "example_CEC2013_benchmark.cpp"

5- Add the reference to hvcmo20a:

	#include "HillVallEA/hvcmo20a.h"

Later, instead of creating a hillvallea object as:
	
	hillvallea::hillvallea_t hillvallea(...);

create a hvcmo object as:

	hillvallea::hvcmo_t hvcmo(...);

6- Consequently set 'local_optimizer_index' and 'cluster_alg' for your hvcmo object.

7- Invoke the execution of the optimizer by telling the id for the current run:

	hvcmo.run(run+1);

Such an id has no serious impact; it is used only to form some names for output files.

8- Run the script.

# Licence

The extensions of HVcMO with respect to HillVallEA are available here under the same GNU General Public License v3.0.
