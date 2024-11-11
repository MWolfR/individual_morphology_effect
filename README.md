# individual_morphology_effect
Quantifying and modeling the effect morphological variability has on connectivity

## Usage:

### Effect of individual axons and dendrites

1. Run the notebook Analyze connectivity higher order sources. Estimated duration: 5 minutes. This notebook performs analyses on a connectome, provided as an input conntility.ConnectivityMatrix object. The results are pandas objects that will be stored in a hdf5 file. Locations of inputs and outputs are directly parameterized inside the notebook and you will most likely have to update some paths for your system. See also "Data sources" below

2. Run the notebook Plot connectivity higher order sources. Estimated duration: 1-2 minutes. This will load the data and compare higher-order connectivity trends from two data sources, and generate plots. It is used to compare specifically the "human" to the "rat" model connectomes (touches).

3. Run the notebook Microns connectivity higher order sources. Estimated duration < 1 minute. It will also load data from the file generated in step 1 and generate plots. It will plot similar plots to the notebook in step 2, but only one data source at a time. The purpose is to show results for the MICrONS connectome, demonstrating that the rules we observe in the model are also in a biological connectome. It is also used to generate plots for a control connectome, demonstrating that simple rules do not capture the trends.


#### Data sources:
 - "human": The touch connectome (all appositions, not pruned) for a human microcircuit model
 - "rat": The touch connectome (all appositions, not pruned) for a rat microcircuit model of approximately the same scale as the human one
 - "microns": The Microns connectome data (v1181)
 - "control": A third order stochastic connectome, fit against the human model above.
 
 
#### Generated plots:
  - cmp_prior_posterior_probabilities.pdf: The statistical effect of the nearest neighbor of a neuron being connected. First row: Incoming and outgoing connection probabilities for human and rat model. Second row: Same, but conditional probabilities as follows: For incoming connectivity, the connection probability A <- B if the spatially nearest neighbor of B innervates A. For outgoing connectivity, the connection probability A -> B if the spatially nearest neighbor of B is innervated by A. Third row: Difference between the first two rows.
  
  - cmp_effective_prob_difference.pdf: Statistics on the values depicted in the previous plot. Depicted is a histogram of the differences shown in the third row of the previous plot, weighted by the number of edges in each spatial bin. Dashed lines indicate the respective means. Colors as indicated in the legend.
  
  - cmp_touch_count_correlations_with_nn.pdf: A different way to depict the trends. Instead of the difference between prior and posterior connection probability it is the correlation of number of touches between a neuron at a given spatial offset and its nearest neighbor. I.e. correlation between the number of touches in A -> B and A -> NN(B), or A <- B and A <- NN(B), where 0 is used if no connection exists.
  
  - spatial_bins_correlations_$SOURCE.pdf: $SOURCE is a place holder for one of the sources listed above. For that source we show the pearson correlation over individual neurons of their connection probabilities from and to spatial bins. Indicated are correlations between the spatial bin indicated by a blue dot (each row is one example) and all other bins. Red colors do NOT indicate that the bins have similar connection probabilities, but that the bins are likely to be innervated together by the same neuron, on top of their individual connection probabilities. Left column: For outgoing connectivity; right column: incoming connectivity. Data for (spatially) upwards/downwards connections are indicated in the upper/lower half of each plot for both columns. Hence the locations of the blue dots appear mirrored between incoming and outgoing columns but still indicate the same relative offset.
  
  - spatial_bins_clustering_$SOURCE.pdf: Based on the data in the previous plot. We used the Louvain algorithm to group spatial bins into clusters based on the correlations of their connection probabilities. Left for incoming, right for outgoing connectivity.
  
  - spatial_bins_clustering_matrices_$SOURCE.pdf: The matrices of correlations of connection probabilities between spatial bins, sorted by cluster ids. Red lines indicate borders between clusters.
  
  - prior_posterior_probabilities_$SOURCE.pdf: as cmp_prior_posterior_probabilities.pdf above, but instead of comparing human to rat, it only shows results for one data source.
  
  - touch_count_correlations_with_nn_$SOURCE.pdf: as cmp_touch_count_correlations_with_nn.pdf above, but instead of comparing human to rat, it only shows results for one data source.
  
  
### Patch sample experiment

The notebook Patch_sample_triad_overexpression conducts various in silico patch sample experiments on the connectivity of a ConnectivityMatrix object. It validates sampled connection probabilities by conducting a sampling that matches Peng et al. in terms of the relative locations of neurons sampled. Then it conducts patch experiments of pairs of neurons further and further apart to show that the overexpression of reciprocal connectivity increases for larger distances.

It also counts triad motifs.


