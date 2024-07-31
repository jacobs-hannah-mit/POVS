# to run POVS
pull this github code to get the file used for this example data
Brain_Cerebellar_Hemisphere_perind_numers.counts.gz

first, download docker for desktop:
https://www.docker.com

then run:
docker pull hnjacobs/python-11-image-hj:v1
docker run -it hnjacobs/python-11-image-hj:v1

then in the terminal:
python3 run_optimizer_alt_ss.py --tissue "Brain_Cerebellar_Hemisphere" --filter_file alt_ss_for_EF_algorithm.csv.gz --tissue_file Brain_Cerebellar_Hemisphere_perind_numers.counts.gz --output_file output.csv

or for skipped exons
python3 run_optimizer_SE.py --tissue "Brain_Cerebellar_Hemisphere" --filter$ 

https://gtexportal.org/home/downloads/adult-gtex/qtl and download 
GTEx_Analysis_v8_sQTL_phenotype_matrices.tar
to get the count data for all other tissues
