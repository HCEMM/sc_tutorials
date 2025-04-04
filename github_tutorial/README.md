# GitHub Tutorial and Tips

Welcome! This tutorial was developed for employees developing data analyses and software in the context of Biotech, and intends to provide some tools for common bioinformatics tasks.

The **version control** system allows you to track changes in code and collaborate with others. It is implemented in Git, a distributed version control system. GitHub is a web-based platform that hosts Git repositories and provides additional features like issue tracking, pull requests, and CI/CD.

**CI/CD** stands for Continuous Integration and Continuous Deployment. It is a software development practice that allows you to automate the process of testing and deploying code changes. This includes keep your software up to date in package repositories, such as PyPI, CRAN, Bioconductor, and DockerHub.

**GitHub Actions** is a feature of GitHub that enables you to set up CI/CD pipelines directly in your repository, as well as other automated workflows. 

---

## 1. Creating a Repository on GitHub  

1. **Log in to GitHub**: Go to [GitHub](https://github.com) and log in to your account.  
2. **Create a New Repository**:  
    - Repositories related to HCEMM can be created [here](https://github.com/organizations/HCEMM/repositories/new).
    - Fill out the form:  
      - **Repository name**: Choose a unique name for your repository.  
      - **Description**: Provide a brief description of your project.  
      - **Visibility**: Choose between public or private.  
      - **Initialize with a README**: Check this box to create a `README.md` file.
      - **Add a `.gitignore`**: Select a template based on your project type (e.g., Python, R).
      - **Choose a license**: Select a license that suits your project (e.g., MIT, Apache 2.0). More information [here](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/licensing-a-repository).
    - Click **Create repository**.
3. **Clone the Repository Locally**:  
    - Copy the repository URL (HTTPS/SSH).  
    - Open a terminal in VS Code and run:  
      ```bash
      git clone <repository-url>
      cd <repository-name>
      ```  

---

## 2. The Version Control Workflow


1. **Check repository status**:  
    ```bash
    git status
    ```  
    This shows changes in your working directory in a very comprehensive way.

2. **Stage changes, commit them and push the commit**:

    After making changes to your local repository, you need to inform GitHub about them, prepare a commit, and push it to the remote repository. 
    
    Once in the remote repository, the changes will be available to all collaborators, which can pull them to their local repositories. 
    
    This is the basic lifecycle of a GitHub repository.
    ```bash
    git add <file-name>     # Stage a specific file
    git add .               # Stage all changes
    git commit -m "Your commit message"   # Use a comprehensive message, might be helpful for future reference!
    git push origin main    # Push changes to the remote repository (the one hosted at GitHub)
    ```
    This commands informs Git locally about the changes you want to include in the next commit.

3. **Pull Updates from GitHub**:

    If you are collaborating with others, you may need to pull updates from the remote repository every once in a while, especially when you intend to make a new commit. This will make sure you are working with the latest version of the code.  
    ```bash
    git pull origin main
    ```

4. **Branching**:

    Branching allows you to work on different features or fixes without affecting the main codebase.  
    ```bash
    git checkout -b <branch-name>   # Create and switch to a new branch
    git checkout main                # Switch back to the main branch
    git merge <branch-name>          # Merge changes from the branch into the main branch
    git push origin <branch-name>    # Push the branch to GitHub
    ```

### 2.1. In an IDE

This workflow can be easily run in most IDEs. The following video shows how to do it in VS Code. (in GIF format, from the local repo)

![GitHub Workflow in VS Code](./resources/version_control.gif)

---

## 3. GitHub Actions: CI/CD  

[GitHub Actions](https://github.com/features/actions) allows you to automate workflows like testing and deployment.

1. **Set Up a Workflow**:  
    - Create a `.github/workflows/ci.yml` file in your repository.  
    - Example for Python testing:  
      ```yaml
      name: CI Pipeline
      on: [push, pull_request]
      jobs:
         test:
            runs-on: ubuntu-latest
            steps:
              - uses: actions/checkout@v3
              - name: Set up Python
                 uses: actions/setup-python@v4
                 with:
                    python-version: '3.9'
              - name: Install dependencies
                 run: |
                    pip install -r requirements.txt
              - name: Run tests
                 run: |
                    pytest
      ```  

2. **Deploy with GitHub Pages**:  
    - Go to the repository settings > Pages.  
    - Select the branch and folder (e.g., `main` and `/docs`).  
    - Push your static site files (e.g., generated by Jupyter Book or Sphinx) to the `/docs` folder.  

---

## 4. The `.gitignore` File  

The `.gitignore` file specifies files and directories to exclude from version control. Example for biotech projects:  
```
# Python
__pycache__/
*.pyc
*.pyo

# Data
*.csv
*.tsv
*.xlsx

# Environment
.env
*.venv/
```  

---

## 5. Licensing and Citation  

1. **Add a License**:  
    - Choose a license (e.g., MIT, Apache 2.0) based on your project needs.  
    - Add a `LICENSE` file to your repository.  

2. **Enable Citation**:  
    - Add a `CITATION.cff` file for proper citation. Example:  
      ```yaml
      cff-version: 1.2.0
      message: "If you use this software, please cite it as below."
      authors:
         - family-names: Doe
            given-names: John
      title: "Biotech Analysis Toolkit"
      version: 1.0.0
      doi: 10.1234/example.doi
      ```  

---

## 6. README File  

The `README.md` file is the first thing users see. Include:  
- **Project Overview**: Brief description of the project.  
- **Installation Instructions**: How to set up the environment.  
- **Usage**: Examples of how to use the software.  
- **Contributing**: Guidelines for contributing to the project.  

---

## 7. Additional Tips for Biotech Developers  

- **Data Analysis Pipelines**: Use tools like Snakemake or Nextflow for reproducible workflows.  
- **Documentation**: Use tools like Sphinx or Jupyter Book for detailed documentation.  
- **Environment Management**: Use `conda` or `virtualenv` to manage dependencies.  
- **Data Security**: Avoid pushing sensitive data to GitHub. Use `.gitignore` and `.env` files.  

---

Happy coding! 🚀  