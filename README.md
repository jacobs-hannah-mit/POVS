# partial pooling variable splicing (POVS)

Partial pooling of variable splicing is an optimization package that fits parameters to observed splicing outcomes across population data. In this tutorial, you will copy a set of filtered splice sites and also the RNA counts data associated with these splice sites and generate an output file that contains information about the fit for each splicing event to the parameters. 

FYI: this project involves using Docker to run a specific Python environment and execute a script with provided data files. Follow these detailed steps to complete the project. Docker is a useful tool because it allows you to not have to worry about version control or anything like that, but it is an extra software to download onto your machine. 

So first, download docker and its desktop application. This will allow you to pull docker images from docker hub, where this image is hosted. 


## Step-by-Step Instructions

### 1. Pull the Docker Image

Open the terminal on your laptop and execute the following command to pull the required Docker image:

```
docker pull hnjacobs/python-11-image-hj:v1
```

### 2. Run the Docker Container

Run the Docker container using the command below. This will start an interactive terminal session within the container:

```
docker run -it hnjacobs/python-11-image-hj:v1 /bin/bash
```

This is now a docker terminal, it should have a # next to it, and you are now in the image. 

### 3. List All Docker Containers
IMPORTANT: Open up a second terminal. 

This will allow to copy the files from this Github Repo that you will clone into your local machine, into the docker image on your machine.

Next, you need to find the location of your docker container. Execute the following command to list all Docker containers. Note the CONTAINER ID of the running container:

```
docker ps -a
```


- **For example, you might see an output similar to:**

> CONTAINER ID   IMAGE                                          
> b0ad28d298b2   hnjacobs/python-11-image-hj:v1   

- Copy the CONTAINER ID (*e.g.*, **b0ad28d298b2**).

### 4. Copy Data Files to Docker Container

After you obtain the files using git clone for this repo, the docker cp command to copy the necessary data files from your local machine to the Docker container. Replace **b0ad28d298b2** with your actual CONTAINER ID:
Make sure you are in the directory where these files are in your machine (in the github repo clone)
```
docker cp alt_ss_for_EF_algorithm.csv.gz b0ad28d298b2:/home
docker cp Brain_Cerebellar_Hemisphere_perind_numers.counts.gz b0ad28d298b2:/home
```

### 5. Execute the Python Script
Now go back into the terminal where your docker container is running.

Inside the Docker container, run the run_optimizer_alt_ss.py script with the appropriate parameters. This command processes the input data and generates the output:

```
cd home
python3 run_optimizer_alt_ss.py --tissue "Brain_Cerebellar_Hemisphere" --filter_file alt_ss_for_EF_algorithm.csv.gz --tissue_file Brain_Cerebellar_Hemisphere_perind_numers.counts.gz --output_file output.csv
```

If this is running correctly, you should see the program running and timing the total runtime on your docker terminal. The total run time is around 5 min for a high performance computer (64 GB RAM, 8 CPUs, i9).

Note that you can do the same thing with skipped exons, you just need to run :

```
cd home
python3 run_optimizer_SE.py --tissue "Brain_Cerebellar_Hemisphere" --filter_file skipped_exons_w_gene_names_and_assigned_abc_introns.csv.gz --tissue_file Brain_Cerebellar_Hemisphere_perind_numers.counts.gz --output_file output.csv
```

### 6. Save the Resulting Output File

After the script completes, the results will be saved in output.csv within the Docker container. Use the following command to copy this file from the Docker container to your local machine:

```
docker cp b0ad28d298b2:/home/output.csv <local directory>

```

This command saves output.csv to the current directory on your local machine.


By following these steps, you will have successfully pulled a Docker image, run a container, copied necessary files into the container, executed a Python script, and retrieved the output file. 


