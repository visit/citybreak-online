# CB Online BodyCssClasses

Citybreak Online inserts some CSS classes into the class attribute of the Body element based on what section of Citybreak Online is active. This enables you to do special styling based on the currently active section, and these values are also accessible from javascript. It also inserts the currently active language. 
The body tag always has a class of *cb_citybreak_body* when Citybreak Online is active.

### Language

The currenly active language is inserted prepended by cb_lang_ , e.g *cb_lang_sv* or *cb_lang_en*


### Section

The currently active section is indicate with a cb_ prefix followed by the name of the section. The following values are used:

Section | Class
--------- | -----------
Accommodation | cb_accommodation
Basket | cb_checkout
Basket & Payment pages | cb_basket
Payment page | cb_basket cb_progress
Events | cb_event
Todo | cb_activity
Ferry | cb_ferry
Add-ons / Complementary information | cb_complementary
Packages | cb_package
