# Templates

The following templates should be used in the creation of new projects.

## Editor Config
An [Editor Config][editor-config] template is provided that can be placed in the
root directory of a project. This base template file will be maintained in this
repository, ideally changes that are needed and not unique to the project will
be discussed and implemented in this template.

* [.editorconfig](.editorconfig)

## Copyright/License
Prior to creating the new project repository in Github, the [Copyright Disclosure Form][copyright]
must be filled out and signed by the entire development team, and then emailed
to the Office of Innovation and Commercialization (OIC).

Once the copyright disclosure form has been turned into OIC, proceed with
creating the new public repository in the [UCSD Library
Organization][ucsdlib] using the following templates.

* [UC Copyright Notice](UC_Copyright_Notice.txt)
* License - Choose MIT from Github license listing.

## Linters
Linter templates, such as Hound and Rubocop, may be used as starting points for
customization as required for the project. For example, Samvera-based projects
may need a separate set of linting requirements than a standard Rails
application. Other additional linters should also be used as required for the project.

Also note that if linters are added to an existing project, it may be necessary
to generate, in the case of rubocop, a `todo` file so that the project can be
slowly cleaned up over time.

* [Hound](.hound.yml)
* [Rubocop](.rubocop.yml)

[copyright]:http://invent.ucsd.edu/invent/researchers/reporting-new-innovation/copyright-disclosure-form/
[ucsdlib]:https://github.com/ucsdlib/
[editor-config]:https://editorconfig.org
