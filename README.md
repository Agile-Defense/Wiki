## Setup Project
1. Install `npm` and `git` on your machine if you don't have it.
   - You can get npm through [Node.js](https://nodejs.org/) for your platform.

2. Setup Wiki Docs project with Git:

```bash
# Clone repo
git clone https://github.com/Agile-Defense/AgileDefenseWiki.git
cd AgileDefenseWiki/

# Install NPM dependencies
npm install

# Run test server on localhost
npm run start
```

## Additions/Modifications

The main pages for the wiki are located in the `content/docs` directory of the project root. To make a new top-level section like `Provisioning` or `Pipelines`, just create a new directory in `content/docs`. 

To allow for default redirects to the head of the section, add `_index.md` in the directory, otherwise add `*.md` files as needed for each subsection. Use what already exists as examples.

## Deploying Changes to the Site

Once you've made the changes or modifications you need, first ensure that the changes get committed by running: 

```bash
git commit -am "Your Commit Message Here" && git push
```

Once changes are committed so they're not lost, deploy via:

```bash
npm run deploy
```

**Congratulations!** Your changes are now live at https://agile-defense.github.io


## Documentation

Agile Defense Wiki utilizes Doks, Hugo, and Netlify

- [Netlify](https://docs.netlify.com/)
- [Hugo](https://gohugo.io/documentation/)
- [Doks](https://getdoks.org/)

### Documentation Communities

- [Netlify Community](https://community.netlify.com/)
- [Hugo Forums](https://discourse.gohugo.io/)
- [Doks Discussions](https://github.com/h-enk/doks/discussions)
