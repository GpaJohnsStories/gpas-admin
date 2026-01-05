# **New GpasSites Design Rules**

## **GENERAL RULES – Updated: 1/5/2026**

1. Public and admin sites share no components    
2. Public headers, and accessibility tools **MUST** use iframes —   
   Example:   
       \<iframe src="kids-menu-header.html"\>\</iframe\>    
3. Public footers and static text blocks **MUST** use fetch \+ innerHTML —  
   Example:     
      fetch("kids-footer.html")  
      .then(r \=\> r.text())  
      .then(html \=\> footer.innerHTML \= html);  
4. Story cards and product cards are site‑specific    
5. Frequently used pages may use hard‑coded text for performance  
6. All future coding will be with only html and javascript, there will be no external css, tsx or ts files created. Styling must be done using inline \<style\> blocks inside each HTML file.  
7. Any section that is reusable in different pages should be created as stand alone and then loaded whenever it is needed. This way one change to any of these reusable sections will change all pages whenever they are loaded.  
   These reusable sections include, but may also include others as we think of them…  
   kids-menu-header.html   
   kids-footer.html  
   super-av.html  
   (kids-break, high-contrast, and page-top) all of these 3 functions contained in one floating semi-transparent vertical box on the right side of the screen.  
8. Each recreated website file will contain these sections, in this order to provide consistency, readability and long-term maintainability…  
   a \- \<head\>\</head\>  
   b \- \<style\>\</style\>  
   c \- \<body\>\</body\>  
   d \- \<script\>\</script\>  
9. Each html file must be **HEAVILY** documented using clear, descriptive comments to explain what each function or group of codes is doing. Comments **MUST** also be used to clearly mark major sections, webtext placement, anchors, and reusable blocks to make it easy to search, understand, and maintain. This especially includes placement of **webtext codes and anchors.**  
10. All recreated html pages must use the same colors and ui design as the original tsx file.  
11. All webtext boxes and stories will be stored in github repos. I will give you the api keys and directory structure when needed.  
12. Supabase will be retained for the story table with its indexes. Once all webtext and stories are moved to github, the content field from the stories table will be deleted. Other current supabase tables may either be migrated to github, left as is or hard coded. This will be decided and the work done on a web page by page basis by Grandpa John.  
13. All of gpas websites will use 4 fonts only \-- Kalam for fun, Lexend for Titles, Georgia for Stories and Gloria Hallelujah, cursive; color: \#0B3D91 only for grandpa john's personal notes and signature.  
14. ALL Story files will be reformatted and migrated by Grandpa John to PDF files using MS Word to format and embed any photos and to format fonts, paragraphs, titles, etc. The story will then be uploaded as a full, print-ready PDF that includes fonts, etc. to proper github directory using the 7 digit code stored in the supabase story index.  
15. ALL Webtext that is NOT hardcoded into a page will be reformatted and migrated by Grandpa John to HTML files using a new admin tool taken from super-text to create clean html for the entire box, including titles, photo links, etc. These will be stored in their own directories on github with a 7 digit code similar to what is being used now.

    No inline junk

    No nested spans everywhere

    No mystery classes

    No hidden scripts

16. All icons will be migrated by Grandpa John from supabase to github where they will be separated into 2 directories \-- site code/icons-core/ or site code/icons-other/ and all file names will begin with "ICO", none with "\!CO". Each website, kids, faith, shop, admin, will have its own icon directories so if an icon is used in more than one site, it will be in github more than once.

## 

## **SPECIFIC GPASKIDS SITE RULES**

1. **FIRST** — Recreate the **gpaskids title/menu bar** as kids-menu-header.html, including the vertical menu  
2. **THEN, when \#1 is complete,** recreate the **gpaskids footer bar** as kids-footer.html.  
3. **THEN, when \#2 is complete,** recreate the **home or index file** as kids-home.html (I will be using specific directory and file names for the url's instead of relying on default of index.html  
4. Except for story cards, replace all webtext with hard-coded text within the html file.

