# Let's dig in

## Multiplicity

Multiplicity happens to be typical for some substances, e.g. list elements or some blocks sequence.

In CSSG it will look like this:
```css
/*

    post_cnt
    	post_cnt_ul
    		post_cnt_li +

*/
```
or like that:
```css
/*

    post_cnt
    	post_cnt_i *

*/
```
The main difference between '\+' and '\*' is in multiplicity specifics.  
'\+' says that element will appear at least 1 time (which is typical for list items - \<li\>)  
'\*' however says that element may appear more than 0 times (any other elements - you name it)

> it's important to feel the distinction between optional elements ([element]) and appearing 0 and more times (element \*)  
> insignificant on the first sight, it appears to have contextual meaning

## Modificators - more and meaningful

As it was mentioned in [basic](basic.md), modificators complement substance and theoretically their simultaneous presence is possible.  
Crucial logic described with the help of special syntax.

For example, alternative is illustrated this way:
```css
/*
	
    post                            ( __current | __regular ) __deleted

*/
```
and even like this:
```css
/*

    post                            ( ( __current | __regular ) | __compact ) __deleted

*/
```
Dot (.) illustrates robust connection between class and another class or modificator
```css
/*

	post 							__compact __featured
		post_h
			post_h_tx . __bold
		post_b
			post_b_cnt
				...

*/
```
> alignment on the right for connected class is not necessary

## Inheritance

Substance can be direct descendant of other substance.  
To point this out, define ancestor via "@" symbol.
```css
/*

   	post-advanced @ post
   		post-advanced_h
   		post-advanced_b

*/
```
> it's not necessary to list all modificators, because they inherited by default  
> however, if there is any difference, we must list all possible classes  
> it's accepted that these defined modificators will only be possible

For instance, it is illustrated in the following code, that **post-advanced** will have one possible modificator **__new**, regardless the fact, that **post** has some modificators as well
```css
/*

    post-advanced @ post                __new
   		post-advanced_h
   		post-advanced_b

*/
```
## Nominal templates

Inheritance is directly connected with nominal templates.  
We simplify illustration of descendant substance and avoid code duplication by setting changeable parts in ancestor substance.  
This is not mandatory, but turns out to be helpful if you have at least two such substances.

As an example, let's say ancestor substance looks like this:
```css
/*

    post
        post_cnt
            % content %

*/
```
or like this, if there is any default content 
```css
/*

    post
        post_cnt
            % content %
                post_cnt_i

*/
```
descendant substance
```css
/*

    post-advanced @ post

    % content
        post-advanced_cnt
            post-advanced_cnt_i

*/
```
> when "filling" the template second % symbol is unnecessary

In this case **post-advanced\_cnt** will be inside **post\_cnt** and will override default content from second code piece.  
Without nominal templates, CSSG may look like this:
```css
/*

    post-advanced @ post

	    post_cnt
	        post-advanced_cnt
	            post-advanced_cnt_i

*/
```
There's almost no difference in this case.  
However all notation potential can be seen in context of describing more complex structure

> the **% content %** element has no DOM implementation, it is just a template name

## Dynamics

By dynamics it's meant that some class or element may appear in layout due to scripts and user activity.
```css
/*
 
    post 					$__disabled | $__active
        post_h
        post_b
            post_cnt

*/	
```
To define dynamic blocks complemented syntax for optional parts is used:
```css
/*
 
    post
    	$[post_msg] 					
        post_h
        post_b
            post_cnt
            	$[post_cnt_msg]
            		post_cnt_tx
            	$[/post_cnt_msg]

*/	
```
## It's <<omplicated

Complex CSS approach can be described with CSSG.

Alternative (mutual exclusive) blocks example:
```css
/*

    post
        post_b
            
            [1]
            post_cnt
            	post_cnt_lst
            
            [2]
            post_cnt2
            	...

            [/]
		
*/
```
When it's necessary to illustrate some valueable class somewhere on the upper level in DOM tree:
```css
/*
	
	blog . __complex	
	
	///
	
    post
        post_b
            post_cnt
 
*/
```
CSSG is self-explanatory _as a rule_, but some tough situations may require comments:
```css
/*

    post
        post_h (1)
        post_b
            post_cnt (2)
    _______________________________________________
 
    (1) comment on post_h
    (2) another comment

*/
```

Proceed to [legend](legend.md)
