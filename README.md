# EX188 Notes
Notes and Lesson Learnt from EX188

I've taken the exam on 17th May 2023 for EX188V4. The following tips and hints may not be applicable in the future if there is any revision to the exams. This note will be left unmaintained and no future updates are expected.

## Exam Content
The following topics were not tested:
- Podman Compose
- Openshift
- Multi-stage Containerfile
- SELinux and container permission related stuff

Each task is to test on the following objective:
- Implement images using Podman
- Manage images
- Run containers locally using Podman
- Run multi-container applications with Podman
- Troubleshoot containerized applications

I've taken the exam on 15th June 2023 for EX188 V4 and assigned with Exam domain number 4. There are 6 tasks in total with sub-tasks within each task to be completed within the 2 hour 30 minutes time frame.
## Exam Task
- Running Simple Containers
- Interacting with Running Containers
- Injecting Variables
- Building Images
- Running Multiple Containers
- Troubleshooting

## Tips
There are about 5 or 6 questions to test on the above objectives, if you're confident, spend less time and quickly complete all the questions to save more time to tackle the Troubleshooting question. I took about 1.5 hours to identify the issues within that task.

Be careful when stopping and removing containers during the Troubleshooting questions. The container names are similar to the previous questions, with an append of <CONTAINER-NAME>-ts. Remember that your containers have to be persisted! Don't accidentally delete containers of the previous tasks.

There is a list of verification tasks after each question. It's not mandatory but recommended to do to verify your solution.
  
During troubleshooting, sudo commands can't be run, such as `sudo nsenter -t <PID> -n ss -pant`.
That being said, `podman exec <CONTAINER_NAME> ss -pant` will also return error.

There is no multi-stage Containerfile, but know the difference between ENV and ARG and how to use ARGs at build time. Also know that ARGs can be passed as variable in build time by executing:
`podman build -t <IMAGE_NAME:TAG> --build-arg <ARG_KEY:VALUE>`
  
## Tips fresh from oven:
1. just study till chapter 6, skip the rest
2. learn pass in --build-arg in build time
3. learn pass in --env in run time
4. learn to use podman generate kube <container_name> to print kube yaml for debugging purpose
5. validate the solution as much as you can
6. sreen resolution MUST BE 1920x1080, any other solutions will be trimmed or can't display full screen (i was almost killed by shrinked down resolution and size)
7. as long as you can create a good container with
  `podman run -d --rm --name <container_name> -p 8080:8080 --network <netowrk> -v <volume>:/<container_folder> --env <varabile_name>=<value> registry_image`
  you can already pass the exam. 
  and GOOD LUCK!!!

## Tips based on the 6 Task
Rule of thumb for conquering the exam is to attempt everything in each task first and revisit to troubleshoot when you find yourself stuck at a sub-task for more than 5 minutes.

Understand the file directory structure to know when to change directory to carry out podman commands.

The following are the sub-tasks under each task that I did not managed to configured successfully or worth sharing
Under Interacting with Running Containers Section
  - To create two running containers sharing the same container port 8080 and host port 80. 
    I found the following article that might be of help (https://iximiuz.com/en/posts/multiple-containers-same-port-reverse-proxy/)
Under Injecting Variables Section
  - Understand how to update Containerfile with ARG command and pass in '--build-arg=arg=value' during build time with the following command 'podman build -t <image:tag> --build-arg=arg-value -f <Containerfile Name>'
Under Building Images Section
  - You are tasked to update two Containerfile. When building the images, it's advisable to spell out the Containerfile Name with the following command 'podman build -t <registry_or_host_name/image:tag> -f <Containerfile Name>' 
  - To get the full image path (e.g. oci-registry:5000/<image:tag>) from the exam main page, as they only provide the <image:tag> in their instruction. You will need the full image path when updating the Containerfile (i.e. FROM full image path)
  - To know how to write the command in Containerfile to execute .sh file (`sh file_name.sh`)

With all our sharing here, I am confident that you can definitely pass your exam on your first take.
All the best and may the odds be ever in your favour! Fighting!
