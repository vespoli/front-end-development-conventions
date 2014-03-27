front-end-development-standards
===============================

## Coding Standards
Some of these are conventions based on preference and will be followed as part of my project, others are just best practices called out and noted here. The developer should be familiar with best practices in general as this is not meant to be an exhaustive list.

### General
Spaces not tabs. Two of them per tab. Make sure your editor is configured properly. Why?
 
- **Chuck Norris** uses spaces. Two of them.
- You don't want to look like an amateur do you?
- View compression - You can see more
- Transference - That code block you just ripped from the stack overflow... spaces
- JADE hates tabs + spaces - Dont piss off JADE or it'll be a bad day

### JADE

Components containers should usually be generic div's. This way they are more flexible to be contained in an element that will provide further semantic meaning depending on how they are used. No need to be explicit with div so lead with the components class name. Let the caller of the component figure out what the semantics are. Dont wrap components in things like `section` or `aside`. Where it makes sense use elements like `header`s and `footer`s insde the component, but not just for the sake of it.

**Bad**

    aside.foo
        header
            h1 This thing
        section
            p hi there kids
            p.more
                a(href="#") Read More
        footer
        
**Good**

    .foo
        h1 This thing
        p Hi kids
        p.more
            a(href="#") Read More
        
Be sparse with your tags. Light markup is the key to eternal hapiiness

### SASS

#### Naming Convention
Selectors should all be lower case. Dashes for spaces

Extend global styles when modifying a universal pattern. If you have a component that needs specific styles but otherwise inherits the global styles. `ul.listing` becomes `ul.listing.listing-news` or `ul.lisitng.listing-search`. 

#### Selectors
Limit use of ID’s. Even components that are expected initially to be singular in scope may turn out in the future not be.

As much as possible, use parent containers to hook into child elements. 

**Bad**

    aside.callout
        h1.callout-header ...
        span.callout-meta ...
        p.callout-description ...
    
**Good**

    aside.callout
        h1
        //global meta style. can be overridden with `.callout .meta` if needed
        span.meta ... 
        p ...

#### Compass
Use the compass utility to make any declarations that require vendor prefixes. This allows us to keep the prefixes up to date as we update compass.
#### Breakpoint
All media specific declarations should be made using breakpoint. *Most* declarations should use a global SASS variable like `$screen-large` or `$screen-medium`. Occasionally you will need to declare non standard breaks to accomodate a specific scenario but should otherwise be avoided
#### Nesting
Don't go overboard with SASS nesting. It leads to inefficient, bloated and more difficultly overridden code. Component specific styles should however always be namespaces in their component by nesting them in the component container.

**Bad**

    aside.callout{
        ul.listing{
            li{
                p.more{
                    a{
                        span{
                            font-weight:bold;
                        }
                    }
                }
            }  
        }
    }
**Better**

    aside.callout{
        ul.listing{
            li{
                ...
            }
        }
        p.more{
            a{
                span{
                    font-weight:bold;
                }
            } 
        }
    }

**Best**
(Why do we have a specific style for callouts. Does it really need to be a unique case??)

    // in global styles
    p.more{
        a{
            span{
                font-weight: bold; 
            }
        }
    }

#### Global vs Component level styles
*Most* general element styles should be accounted for in the global styles. Any component specific styles should be namespaced in the component's wrapper.

    .some-component{
        h1{font-family: $sans-serif;}
        a{color:green;}
    }

### JavaScript
#### Naming Conventions
Variables and method names should be lower camelCase. Only classes should use upper CamelCase.

    var yourMomma = new FOO.YourMoma();
    yourMomma.layOnGuiltTrip();

jQuery object variables should always be preceded by `$` ie:

    var $this = $(this);

    
#### Namespace
All JavaScript code for your application should live under your applications namespace which is initialized in /src/js/app.js along with any global utility functions that are part of the application. Use something short like the initials of the project.

#### jQuery vs Backbone listeners
Except in specific scenarios, event listeners should be attached as part of a view’s event object and not via a traditional jQuery event listener. 

TODO: provide examples of specific instances where you should use jQuery

#### Performance
Cache DOM references. If you use an item more than once in any scope, it must be cached in a local variable.
var $this

TODO: Provide references to jQuery performance best practices (even better show super fast lodash equivalents) :

`$(‘.foo’)` vs `$(‘.foo’).eq(0)` vs $`(‘.foo:first’)`

### Browser Testing and Support
All code developed for the front end production should be developed for and tested with the following device/OS/browser combinations. This is just a baseline and may change from project to project

Mac/OSX/Chrome, Firefox, Safari(6.x *)

iPhone 4s/iOS 7/Safari  
iPad 4/iOS 6/Safari  
Samsung/Android 4.3/Galaxy S4

PC/Windows 8/IE10  
PC/Windows 7/Chrome, Firefox, IE9

-All browsers and OS except where specified are latest non beta release


