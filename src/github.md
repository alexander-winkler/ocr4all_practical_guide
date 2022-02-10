# Collaborate via Github

The easiest way probably is to create a clean OCR4all docker container for the project you want to collaborate on via Github.

Two different scenarios are presented: 

1. You create your project and share it via Github
2. You join an existing project and contribute to it

## Scenario I: Create your own project

### Prepare your system

Create your project folder and `cd` into it:

```bash
mkdir -p my_project/{data,models}

cd my_project
```

### Create a git repository locally

In your project folder initialize a git repository and add your files:

```bash

git init

git add .

git commit -m "First commit"

```

### Create a repository on Github

Go to [Github](https://github.com) and create a repository (e.g. `my_project`). 

```bash
git branch -M main
git remote add origin git@github.com:<YOUR-GITHUB-ACCOUNT-NAME/my_project.git
git push -u origin main
```

## Scenario II: The projects exists already

#### Clone an existing repository

If you want to contribute to an existing repository, clone it:

```bash

git clone git@github.com:<SOME-GITHUB-ACCOOUNT>/someones_project.git
```

## Create a new docker container

In both scenarios you now will have to create a new docker container with the right mappings.
If you don't want to remove your default docker container, you have to give it a different name, here `ocr4all_my_project`. You might also want to assign a port other than `1476` in order to avoid conflicts if you run both containers contemporarily. Here, we use `1477`.

`cd` into the folder you have created (`my_project` in scenario I or `someones_project` in scenario II).

```bash
sudo docker run -p 1477:8080 -u `id -u root`:`id -g $USER` --name ocr4all_my_project \ # In scnario II:  someones_project
-v $PWD/data:/var/ocr4all/data \
-v $PWD/models:/var/ocr4all/models/custom \
-it uniwuezpd/ocr4all
```

Now, your new docker container is available at <http://localhost:1477/ocr4all/>.

## Do your work

Open your browser at <http://localhost:1477/ocr4all/> and do your work (check line segmentation, add Ground Truth etc.).

It is a good idea to check if your local repository is up-to-date with the remote one.

So, before getting to work, do

```bash
git pull origin main
```

## Stage, commit and push

When you've done some work, push it to the repository:

```bash

git add .

git commit -m "checked OCR for Chap. 1 of XYZ"

git push
```

In case you embark on a more adventurous set of modifications, consider creating a new branch.

```bash

git checkout -b <branch_name>
```

For mere Ground Truth generation, this should not be necessary, however.