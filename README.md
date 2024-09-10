# partial pooling variable splicing (POVS)

This project involves using Docker to run a specific Python environment and execute a script with provided data files. Follow these detailed steps to complete the project.

## Step-by-Step Instructions

### 1. Pull the Docker Image

Open the terminal on your laptop and execute the following command to pull the required Docker image:

```
docker pull hnjacobs/python-11-image-hj:v1
```

### 2. Run the Docker Container

Run the Docker container using the command below. This will start an interactive terminal session within the container:

```
docker run -it hnjacobs/python-11-image-hj:v1
```

### 3. List All Docker Containers

Execute the following command to list all Docker containers. Note the CONTAINER ID of the running container:

```
docker ps -a
```
or
```
docker images
```

- **For example, you might see an output similar to:**

> CONTAINER ID   IMAGE                                          
> b0ad28d298b2   hnjacobs/python-11-image-hj:v1   

- Copy the CONTAINER ID (*e.g.*, **b0ad28d298b2**).

### 4. Copy Data Files to Docker Container

After you obtain the files using git clone for this repo, the docker cp command to copy the necessary data files from your local machine to the Docker container. Replace **b0ad28d298b2** with your actual CONTAINER ID:

```
docker cp alt_ss_for_EF_algorithm.csv.gz b0ad28d298b2:/home
docker cp Brain_Cerebellar_Hemisphere_perind_numers.counts.gz b0ad28d298b2:/home
```

### 5. Execute the Python Script

Inside the Docker container, run the run_optimizer_alt_ss.py script with the appropriate parameters. This command processes the input data and generates the output:

```
python3 run_optimizer_alt_ss.py --tissue "Brain_Cerebellar_Hemisphere" --filter_file alt_ss_for_EF_algorithm.csv.gz --tissue_file Brain_Cerebellar_Hemisphere_perind_numers.counts.gz --output_file output.csv
```

Note that you can do the same thing with skipped exons, you just need to run 

```
python3 run_optimizer_SE.py --tissue "Brain_Cerebellar_Hemisphere" --filter_file skipped_exons_w_gene_names_and_assigned_abc_introns.csv.gz --tissue_file Brain_Cerebellar_Hemisphere_perind_numers.counts.gz --output_file output.csv
```

### 6. Save the Resulting Output File

After the script completes, the results will be saved in output.csv within the Docker container. Use the following command to copy this file from the Docker container to your local machine:

```
docker save -o output.csv hnjacobs/python-11-image-hj:v1
```

This command saves output.csv to the current directory on your local machine.


By following these steps, you will have successfully pulled a Docker image, run a container, copied necessary files into the container, executed a Python script, and retrieved the output file. 
