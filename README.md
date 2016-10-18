[![StyleCI](https://styleci.io/repos/56759262/shield?style=flat)](https://styleci.io/repos/56759262)

# Sitegeist.Monocle

## A living styleguide for Neos

This package adds a styleguide module to Neos that renders the
TypoScript2 prototypes in isolation that are annotated with `@styleguide`.

### Authors & Sponsors

* Martin Ficzel - ficzel@sitegeist.de
* Wilhelm Behncke - behncke@sitegeist.de

*The development and the public-releases of this package is generously sponsored
by our employer http://www.sitegeist.de.*

### Living Styleguide

The Monocle-Module uses the real TypoScript2 code to render the annotated
prototypes in isolation. That way the styleguide is always up to date and cannot
diverge over time from the real codebase.

The Monocle was defined with Atomic-Design and pure TypoScript2 without Fluid in
mind but the implementation is Coding-Style and Template-Engine agnostic. You can
use Monocle to render Fluid based Prototypes without any limitation.

## Usage

### Create items for the styleguide

To render a prototype as a styleguide-item it simply has to be annotated:

```
prototype(Vendor.Package:MyCustomPrototype) < prototype(TYPO3.TypoScript:Tag){
    @styleguide {
        path = 'atoms.basic'
        title = 'My Custom Prototype'
        description = 'A Prototype ....'

        # an optional class for the wrapping div of the preview
        # previewContainerClass = 'class-with-nice-background'

        # render the prototype in a single iframe
        # display = 'iframe'

        # define the height of the prototype iframe
        # height = 600

        # ts props to override for the styleguide rendering
        props {
            content = 'Hello World'
        }
    }

    // normal ts props
    content = ''
}
```

### Configuration

Some configuration is needed to define the JS and CSS that has to be included for the preview.

```YAML
Sitegeist:
  Monocle:
    preview:
      defaultPath: 'atoms'
      additionalResources:
        styleSheets:
          # example:  'resource://Vendor.Site/Public/Styles/Main.css'
        javaScripts:
          # example: 'resource://Vendor.Site/Public/Scripts/Main.js'
```

### Routes

If the default flow subroutes are not included in your main Routes.yaml you can add the following
routes to your global Routes.yaml and only enable the monocle-subroutes.

```YAML
##
# Sitegeist.Monocle subroutes

-
  name: 'Monocle'
  uriPattern: 'sitegeist/monocle/<MonocleSubroutes>'
  subRoutes:
    'MonocleSubroutes':
      package: 'Sitegeist.Monocle'
```
