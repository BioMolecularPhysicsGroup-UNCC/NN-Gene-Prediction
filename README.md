<p align="center">
  <img width="600" height="250" src="https://github.com/jwodder/versioningit/assets/91847580/6ee1a363-ce2b-4d3f-8330-4bb13506f3c2">
</p>

---

# NN-Gene-Prediction - created by Mr. Lonnie Baker
################## NN gene prediction method instructions #####################

Requires python3 and Tensorflow

Many parameters are the same between functions. They are redundant so that saned files passed between functions will be compatible.


1. To run an out-of-the box test use the following commands

python3 Generate_sensor_data.py
python3 Generate_training_dataset.py 
python3 Generate_test_dataset.py 
python3 Train_dense_model.py 
python3 Test_dense_model.py

This will use small sample fasta and gff3 files (included) to train and test the method quickly and make sure it is running

#################################################


2. Sensor data

Sensor data must be generated for any DNA which is to be used for training or testing

fasta files must be located in the fasta_files folder. Each fasta file must be a sinlge sequence with a header to be preceded by ">"

gff3 files must be located in the gff_files folder. The first column of each entry in the gff files will be refered to as the "chromosome" name of the entry.

Parameters:


species_list: A list of species you wish to generate sensor data for

chromosome_list: A list of chromosome names. Each species in the species_list must have a single element in this list at the same position in the list. When parsing the gff3 files, this list will specify which chromosomes to use.

kmer_species_list: A list of species which will be used to train kmer frequency sensors. When generating test data, the kmer species must not match the test species.

kmer_chromosome_list: A list of chromosome names. Each species in the kmer_species_list must have a single element in this list at the same position in the list. When parsing the gff3 files, this list will specify which chromosomes to use when training the kmer sensors.

window_size: The nucleotide width of all sensor algorithms to be used.

n_sensors: the number of sensors being used must be specified here

kmer_training_multiplier: sets the level of sampling used when training the kmer sensors. Seeting this to 1 results in a total number of kmers equal to (number_of_possible_kmers)*1000. This number can be set low (=0.001) when doing quick test runs on a personal computer. Setting this number higher than 1 requires significant resources.

#################################################

3. Training datasets

Sensor data must be cut into training and test sets before use.

Parameters:

species_list: must have entries which match previously generated by data from Generate_sensor_data.py

window_size: must match the window size previously used by Generate_sensor_data.py

set_title: use this to name your datasets

n_samples: the total number of samples to train on

positive_fraction: the fraction of positive samples you wish to train on

#################################################

4. Test datasets

Sensor data must be cut into training and test sets before use.

Parameters:

species_list: must have entries which match previously generated by data from Generate_sensor_data.py

kmer_species_list: must have entries which match previously generated by data from Generate_sensor_data.py

window_size: must match the window size previously used by Generate_sensor_data.py

set_title: use this to name your datasets

#################################################

5. Training neural nets

A basic NN with 10 hidden neurons in a single layer is included. This can be modified.

Parameters:

species_list: must have entries which match previously generated by data from Generate_sensor_data.py

set_title: must match a set title which was used to generate a training set

nepochs: the number of epochs to train the NN

Neurons_per_layer: use this to describe the NN architecture once it is saved

Training_fraction: must be of the form "pxx" where xx is an integer which specifies the positive_fraction used in the training set

window_size: must match the window size previously used by Generate_sensor_data.py

cross_validation: the number of cross validation sets to use. Each validation run will train and save a separate NN.


#################################################

6. Testing neural nets

In order to test the accuracy of trained models, sensor data must be previously generated for the test species.

Parameters:

Training_species: must have entries which match models previously trained on these species using the names in species_list used by Generate_sensor_data.py

species_list: list of test species. Must have entries which match species_list names previously used by Generate_sensor_data.py

set_title: must match a set title which was used to generate a training set

Neurons_per_layer: must match Neurons_per_layer string of a previously trained NN architecture

Training_fraction: must match Training_fraction string of a previously trained NN architecture

window_size: must match the window size previously used by Generate_sensor_data.py

cross_validation: must match the number of cross validation steps used to train the models being called

initial_voting_threshold: the lowest CDS/nonCDS threshold to consider

min_cds_length: the minimum length CDS regions to consider

max_cds_length: the minimum length CDS regions to consider

max_cds_threshold: the maximum CDS/nonCDS threshold to consider

threshold_step: how much to increase the CDS/nonCDS threshold at each iteration





