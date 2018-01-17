# Let's begin

CSSG describes substance structure with familiar cascade of CSS classes, using BEM concept in slightly different way.  
Classes naming happens according to accepted rules that you or your company follow.  
Classes standing apart of substance classes are added near main class.  
As a rule, auxillary (cosmetic) classes are not added, except for special cases (described in [advanced](./advanced.md)) 

Along this documentation fictional substance "post" is used as an example.  
Let's assume it's the post in blog or any other block that has head, body, footer and secondary elements.

## Your first CSSG

Let's say your HTML looks something like this:
```html
<div class="post">
	<div class="post_h">
		<div class="post_h_name">Header</div>
	</div>
	<div class="post_b">
		Content
	</div>
	<div class="post_f">
		Additional information
	</div>
</div>
```
CSS looks like that:
```css
.post {
	font-size: 14px;
}

.post_h {
	font-weight: bold;
}
```
etc.

CSSG illustrates HTML structure with CSS terminology and is placed in document _before_ all other rules:
```css
/*
	
    post
        post_h
            post_h_name
            post_h_date
	
        post_b
        	...

        post_f
	
*/

.post {
	font-size: 14px;
}
```
If you've worked with HAML or have idea about it's syntax, this structure will be familiar to you.  
By default all structure elements don't have specific DOM-presentantion, so _class_ is prior to _tag_.  
If it's necessary to exaggerate tag-class connection, habitual zen-coding notation is used:
```css
/*
	
    post
        post_h
            post_h_name
            i.post_h_date
	
*/
```
Few notes on syntax:  
> descendants illustrated by tab  
> siblings separated by extra line in case of having child elements  
> CSSG structure should fit screen height due to viewing comfort

## Key content

Key content is denoted with ellipsis (...), other content is ignored.  
Ellipsis means that there is no nesting or it is not related to described structure.  
Example of incorrect CSSG:
```css
/*
	
    post
        post_h
            post_h_name
            	...
            post_h_date
            	...
	
        post_b
        	...

        post_f
        	...
	
*/
```
Key content can be located near other important substance part:
```css
/*
	
    post
        post_h
            post_h_name
            post_h_date
	
        post_b
        	...
			post_b_author

        post_f
	
*/
```
Apart substance, but still related to project, is denoted with figure brackets.  
Key content, complemented with apart substance, is denoted with ellipsis placed nearby.
```css
/*

    post
        post_h
            {date}
        post_b
            post_cnt
                {... article}

*/
```
## Pseudo elements

When it's meaningful to depict usage of pseudo-elements just use native notation:  
> Just remember about the right placement!

```css
/*
	
    post
        post_h
            ::before
            post_h_name
				::before

			::after
	
*/
```
## Links

In case of complicated structure, it is more convenient to describe structure skeleton with links to compound sections in the beginning of CSS document.
```css
>> CSS start

/*

    post
        #header
        #body
        #aux

*/

>> CSS continues

/* #header

    post_h
        post_h_name
	
*/
```
> link to compound section is denoted by native symbol - #

## Modificators and project classes (mix-ins)

HTML layout changes - due to context or by itself. CSS modificators allow to change substance presentation.  
Modificator in fact is CSS class like **.post\_\_new** or **.\_\_compact**, which is placed near main class.  
Project class (mix-in) allows to re-use substance and is placed separately from main class, e.g. **.post-featured**.

In CSSG all possible modificators placed on the right (aligned independently from nesting level) of target class.  
You choose distance manually, regarding diagram size and reading comfort.  
If project (mix-in) is implied, it is placed _before_ modificators list.
```css
/*

    post                        -project __new __featured
        post_h
        post_b
            post_b              __compact

*/
```
> modificators list in such way points to _availability_ of their simultaneous presence, without extra logic  
> more detailed information about modificators in [advanced.md](./advanced.md)

## Optional parts

Parts of substance, that may absent (or not compulsory for current substance) are enclosed in square brackets.  
If it's single class, brackets placed on the same line, on the contrary they are placed on separate lines for more convenient reading.
```css
/*

    post
        [post_teaser]
        post_h
        post_b
            [
            post_b_top
                post_b_top_tx
            ]

*/
```
If optional part is a wrapper, following syntax is used:
```css
/*

    [post_w]
        post
            post_h
            post_b
				[post_b_cnt]
            		[post_b_tx]
            			...
            		[/post_b_tx]
				[/post_b_cnt]
    [/post_w]

*/
```
> hyphens and spaces are not dogmatic in this case. Mind code purity and reading comfort in the first place.  
> furthermore, team might want to choose single syntax, equal for every member.

## Persistent blocks

Practically, large project or framework implies structures, that remain contant in spite of context. 
Examples of such structures - button, form element, social widget etc.

When they can't be ignored or on the contrary - it's _necessary_ to illustrate their presence - following syntax is used:
```css
/*

    post
        post_h
        post_b
        post_f
            post_f_ac
                <social>

*/
```
> it is important to make up list of persistent, re-usable blocks  
> developers team should obtain single list of blocks

Proceed to [advanced](./advanced.md)

-----

[cssg.rocks](http://cssg.rocks) 2015 - 2018  
[github](https://github.com/CSSG/)
