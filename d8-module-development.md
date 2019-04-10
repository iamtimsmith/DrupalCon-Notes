# Introduction to Drupal 8 Module Development - Michael Anello

## Michael Anello
- [DrupalEasy](drupaleasy.com)
- ultimike on drupal.org (drupal.org/u/ultimike)
- @ultimike
- [Find Notes from speaker here](https://docs.google.com/document/d/1d1MbagzcR562-DZS2kJedYuXyTLiML5qJ0XECIjpEtI/edit)

## Notes
- In OOP, Objects/Classes: Same thing
- Using Drupal Console automatically sets stuff up with PSR-4 (php community standard)
- Plugins are classes that you put somewhere and they "just work", but must reside in specific directories to work
- Annotations are cached when cache is rebuilt so it doesn't have to call classes each time. Huge performance gain.
- Annotations are not read at runtime. If annotation is changed, cache needs to be rebuilt.
- Migration commands are only in drush, Drupal Console good for modules
- Symfony: A set of PHP components
- Composer: Dependency manager for PHP
- [Drupal-composer](https://github.com/drupal-composer/drupal-project): Composer setup of Drupal
- Routing YAML files get cached so any changes need cache:rebuild
- Kint (comes with devel) is new Krumo
- When working with templates, template file name must use hyphen. When calling template in .module, change hyphen to underscore
- In Drupal 7, Menu and Routing were one. In D8, they're separate.


## Learn More About...
- Lando
- DockSal
- DDev