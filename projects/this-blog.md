---
date: 2019-10-06
thumbnail: "/uploads/Cesar134.jpg"
title: About this blog
categories:
- personal development
- blog creation
- static sites
project_bg_color: ''
project_fg_color: ''
journal:
- journal/that-first-commit.md

---
I guess it all starts with me wanting a showroom for my projects and experiments.

## The requirements

The requirements for this project looked complex at the begging:

* Needs to free
* I should be able to jump in the whole code and edit it:
  * Avoid non-frontend solutions
  * Avoid know PHP solutions (as Wordpress or Drupal)
* It needs to be static and minimal

At the end, all I want is a static space where to put some text with some style, I shouldn't be on the need for a database, complex infrastructure or external developers to allow me to add themes via "plugins", "themes" or "add-ons". I just need storage and a content manager.

## My solution

For **storage** I chose [**https://github.com**](https://github.com "https://github.com") as it's my public portfolio showroom as a developer. It provides version control, but it also hosts the files for free allowing me to not have to pay for a **hosting service**, if I could I would have used Github pages replacing the need to pay for storage or traffic.

And as a **content manager** I chose [**https://forestry.io**](https://forestry.io "https://forestry.io") as it works on top of Github and other similar services, providing exactly the bare minimum content management I was looking for.

While starting with Forestry some options are presented about the technology that you want to use under the skin. This will affect to how easy I can jump into the code and modify it.
I chose for my starter to go with [**https://gridsome.org/**](https://gridsome.org/ "https://gridsome.org/"), a framework on top of Vue, that will be rendered on build and generate a static site. A site with Gatsby would do the same, but on top of React.
At this point I chose Vue over React just because of the way the styles are used in Vue, as it's probably the piece of code I change the most.
Gridsome will require building, so Github pages it's not a solution anymore.

Luckily there's [**https://netlify.com**](https://netlify.com "https://netlify.com") allowing us to do **continuous deployment**, which means every time that we update the site, it's going to get redeployed and we'll see the changes.