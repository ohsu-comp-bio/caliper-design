> [!TIP]
> Update the site by editing files in the [docs](./docs) directory! ✍️

## Overview ⚙️

Design docs for the CALIPER components and tools ⚙️

> https://ohsu-comp-bio.github.io/caliper-design

## Quick Start ⚡

```sh
python3 -m venv venv && source venv/bin/activate

pip install -r requirements.txt

# Run locally at http://localhost:8000
mkdocs serve

# Push to GitHub Pages
mkdocs gh-deploy
```

## GitHub Actions 🚀

- [ci](https://github.com/ohsu-comp-bio/caliper-design/actions/workflows/ci.yml): Automatic deployment when pushing to the `main` branch
- [pages-build-deployment](https://github.com/ohsu-comp-bio/caliper-design/actions/workflows/pages/pages-build-deployment): Manual deployment from running `mkdocs gh-deploy`

## Additional Resources 📚

- [git](https://git-scm.com/): Free and open source distributed version control system 
- [git-lfs](https://git-lfs.com/): Git Large File Storage — An open source Git extension for versioning large files
- [dvc](https://dvc.org/): Data Version Control
- [Pandas](https://pandas.pydata.org/docs/getting_started/intro_tutorials/01_table_oriented.html): Flexible and powerful data analysis / manipulation library

## TODO 🌀

- [ ] Expand existing [docs](./docs)
- [ ] Add automatic link checker
- [ ] Add Google Colab examples?
