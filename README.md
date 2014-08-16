# Softcover Cheat

Cheat on [Softcover](https://github.com/softcover/softcover) capabilities.

Tested with: <https://github.com/cirosantilli/softcover_vagrant>.

The most important file is [chapters/chapter1.tex](chapters/chapter1.tex), which will contain every test that can be contained in a single file.

My focus is on using Softcover for small tutorials, without allowing any style configuration. This is not the main intended use case for the software which focuses on large books for sale, and I'm investigating feasibility for tutorials here.

## Pros and Cons

Pros:

-   implements a Markup that I consider to contain the minimal functionality needed for writing tutorials that outputs to both PDF and HTML really well

-   PolyTeX uses LaTeX syntax, so there are plenty of tools to work with it. It only defines a few new macros, but it is all still LaTeX. And in a sense, LaTeX is quite sane: almost all special markup start with a single character: the backslash `\\`, unlike Markdown which has many magic characters, and new magic is needed for every new command.

    The Markdown system is in Softcover if of no interest to me: it is uglier to mix Markdown with LaTeX than having them both separately, and there are already tools that do Markdown to PDF like Pandoc.

    The PolyTeX docs are scarce, but as mentioned in the docs, you can just generate Markdown into PolyTeX and see what it gives to know how to use it: it is quite human readable.

Cons:

-   too much noise. Softcover:

    - generates tons temporary directories and files on the current directory so you lose track of what is important
    - Git tracks tons of customization / HTML view files like the entire MathJax! I am against customization as it makes information harder to find and the system much more expensive to maintain.

    This is specially painful for writing short tutorials instead of huge books, which is my focus, in which case you will have a bunch of projects, and therefore a bunch of boilerplate.

    This could be solved by making a pre processing script that takes the important files, and pastes them into a Softcover template: I'm on the verge of creating such a tool.

-   hard to install.

    There are simply too many dependencies, and only OS X is tested against, not Ubuntu.

    An online compiler service on Git push hook would be an ideal solution.

## Important files

- `Book`: the chapter order
- `chapters/`: contains the chapters, either PolyTeX with `.tex` extension, or Markdown with `.md` extension. All files there will be compiled to PolyTeX files under `generated_polytex`. This means that you can see what PolyTeX Markdown generates.
- `config/book.yml`: `title`, `subtitle`, `author` appear on the book title page.

## Extraneous files

The following files are not gitignored, but can be removed without affecting the build / local view.

- `config/marketing.yml`. Web interface metadata only.
- `media`.                Videos shown / sold on web interface.
- `filename.tex`.         Generated.
- `.softcover-deploy`.    Only used for deployment.

The following files are only used to build / view the output style: if you don't care about customization like me, you can factor them out.

- `epub`
- `html`
- `latex_styles`
- the default `images`:  placeholders, cover which is useless for tutorials,
- `filename.tex`:        whose exact name is set on `config/book.yml > filename`. Output file created from metadata on `Book` and `config/book.yml`, and thus that should be gitignored: <https://github.com/softcover/softcover/pull/116>.
- `config/preamble.tex`: almost anything you put there will only work for PDF, so it does not interest me.
- `config/lang.yml`:     translation of terms

There are also a bunch of temporary files which are probably useful, but which I'd rather move to another directory because they distract me too much on the top-level:

- `texput.log`
- `genearted_polytex`
- `log`
- `tmp`
