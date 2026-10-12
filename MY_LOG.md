# BY PRATEEK GUPTA | 01796402725 | CSE

Hello Guys 🖐️

*Template for me IGNORE*

**Reproduced:**

**Thinking Process:**

**Cause:**

**Fix:**

**Checked:**

**Time:**
----------------------------------------------------------------------------------------

### CC-01 : "The search suggestions are behind everything"

**Reproduced:** Searched Chinese in the search bar, the suggestions were under catTabs div(using inspect tool in edge)

**Cause:** Seems like z-index issue. Yup I was correct, z-index is 40.

**Fix:** Deleted the z-index line.

**Checked:** The suggestions now appear above the bar. *FIXED*

**Time:** about 4-5 min.
----------------------------------------------------------------------------------------

### CC-02: "Can't read anything in dark mode"

**Reproduced:** Don't need to reproduce, the name of the dish and its price is another dark color on a darker background.

**Thinking Process:** Seems like a var(--muted) problem. Searched --muted & name-btn(using inspect in browser) in css file. inspected style of name-btn.

**Cause:** color of the name-btn was being inherited by its parent body named dish-body on 293 line.

**Fic:** Deleted color attribute.

**Checked:** Save & refreshed the css file and browser. *FIXED*

**Time:** about 5-7 min.
----------------------------------------------------------------------------------------

### CC-03: "The menu is wider than my phone"

**Reproduced:** Used Toggle device emulation tool in inspect in edge. Something breaks after shrinking the width past 350px.

**Thinking Process:** maybe there is a media query for this made intentionally, nope. min-width of these card might be 350px, nope. img-wrap's img may have some width issue, I couldn't find any width property that would cause this, though it might not be 350 but 368px = 23rem, nope. Couldn't find anything, I am making another media query specifically for this.

**Cause:** No fallback for menu-cards after reducing width below 350-360px.

**Fix:** made width of menu-card 90% of the viewport width. Also made padding 5% of viewport width so that it stays at center.

**Checked:** The menu-cards are visible even at 160px width or below! *FIXED*

**Time:** 10 - 15 min  
*Found a bug at 481px width EXTRA? --> refer to CC-11 (just after all the mandatory bugs)*
----------------------------------------------------------------------------------------

### CC-04: "The buttons don't work on my tablet"

**Reproduced:** changed width to 768px for tablet width.This behaviour is for 760px - 900px width.

**Cause:** There is an after element that is above btn thus preventing its interaction.

**Fix:** Deleted the media query responsible for this on line 1031 to 1046

**Checked:** Button was already working lol, now user can interact with it directly. *FIXED*

**Time:** 2 min
----------------------------------------------------------------------------------------

### CC-05: "The category bar scrolls away on my phone"

**Reproduced:** shifted to 320px width.

**Thinking Process:** something to do with 'sticky position'. sticky is applied to filter. Its parent has overflow-x. Found it.

**Cause:** Overflow property makes the sticky element stick to it not the page.

**Fix:** (1) Deleted the overflow property for it. (2) added top:91.5px property for sticky;

**Checked:** It does stick, but it sticks to the top. But that will make the filter tab take up half of the screen on smaller devices. *FIXED*

**Time:** >1hr 
*This created a frontend design issue for smaller devices, thus it has to be fixed later --> refer CC14* pending
----------------------------------------------------------------------------------------

### CC-06: "I ordered more than they had"

**Reproduced:** Clicked add to cart and increased the order count for the item where only few(3) were left.

**Thinking Process:** 
> Clearly there is no limit to no. of item's count that can be increamented on these items.
> Found the btn on 153 line in menu.js in frontend.
> I did not knew what data-action is, so I searched it on google.
> went to the inc case on line 234.
> went addToCart() in cart.js ar line 186.
> went to state.js, addToCart() at line 106. addToCart() calls setQty() just above it.
> final: setQty must have another error cond for (if next > dish.stock)

**Cause:** there was no condition check to prevent increment when qty-value increased greater than the stock

**Fix:** added that condition to setQty() in state.js at line 97 (integrated it with)

**Checked:** checked on two items that had low badge acive. *FIXED*

**Time:** about ~4hr
----------------------------------------------------------------------------------------

### CC-07: "Cancelling makes it worse"

**Reproduced:** Ordered A dish and cancelled right away, the no. of dishes dropped when ordered and dropped again when cancelled but never came back in the counter tab. Ordered 2 dish, subtracted 4.

**Thinking Process:**
> went to cancel order btn in indec.html line 268.
> went to staff.js line 104 searching staffRows. Then found cancelled dataset at 154.
>  went to cancelOrder() in orders.js at line 208.
> well, cancelling should be done in the backend,searched cancel in smoke.js, found smthng on line 298.
> went to recommend.js, found smthng good in validation.js at line 118. releaseStock()
> changed - to + to add the stock back.

**Cause:** releaseStock() function subtracted the no. of dished ordered hence subtracting double of what ordered.

**Fix:** Changed - (minus) in the function to + (plus) {- -> +}

**Checked:** Checked multiple dishes in lunch time, each dish contains what it contained before the order placed after cancelling. *FIXED*

**Time:** >1.5 hr
----------------------------------------------------------------------------------------

### CC-08: "An old coupon still works"

**Reproduced:** coupons.json has only one coupon that has expired. Added one more, used both. both apply which they shouldn't because they are expired.

**Thinking Process:**
> searched for coupon in pricing.js, found applyCoupon on line 82.
> I think there is no if statement to validate expiry.
> forgot how to compare two date objects, did a quick google search. used .getTime() to convert string/object to millisecond time and then compared them.
> added and checked.

**Cause:** There was no check for expiry in pricing.js

**Fix:** Added an if statement for it.

**Checked:** Checked using both coupons (The old one and custom one too)

**Time:** 10 min. *There is UTC timezone being used, there has to be some bug around this* pending
----------------------------------------------------------------------------------------

### CC-09: "The menu shows more dishes than it should"

**Reproduced:** check if this was true by using inspect element, and yes there are many articles under menu-grid. There should have been only 6 at fresh reload but there are many.

**What I tried:**
> read dom.js in frontend
> somethign to do with rendering

**Where I got to:**

**What I would try next:** pending
----------------------------------------------------------------------------------------

### CC-10: "Sorting by price is backwards"

**Reproduced:** reloaded the menu, changed filter to (low to high), menu displayed high to low and vice versa

**Thinking Process:**
> menu.js has an event listener for this. it changes filter property in state.
> there is SORTER function in search,js at line 78. it has the value: price-asc and price-desc
> swapped a and b because they do opp things.
> saved and checked

**Cause:** SORTER function in search.js at line 78 had mixed up calculations for sorting.

**Fix:** swapped valued that swapped to make the math correct

**Checked:** Reloaded and changed filter to low to high, it correctly shows low priced one first and same goes with high to low *FIXED*

**Time:** ~15 min
*The focus on the filter dropdown btn cut off below --> refer to C12*
----------------------------------------------------------------------------------------
                                        EXTRAS
----------------------------------------------------------------------------------------

### CC-11: "from width: 480px to around 630px, the menu-grid is wider than the topbar"

**Reproduced:** shifted to 500px width using inspect tool.

**Thinking Process:**
> the grid is becoming 2 column too early.
> the grid goes out of viewport width.
> noticed that when reducing width, at 694px, the width of image gets unequally shrinked, this is not 1fr

**Cause:** the min-width of image got locked because of some reason related to its parent.

**Fix:** added a min-width: 0; in image's parent class to lock it to its parent.

**Checked:** Checked the layout of the grid menu properly in all width sizes. *FIXED*

**Time:** ~45 min
----------------------------------------------------------------------------------------

### CC-12: "Focus line of filter dropdown cuts of in larger screens"

**Reproduced:** clicked the filter dropdown on regular laptop screen.

**Cause:** There is no padding below it thus cuts the focus line.

**Fix:** changed padding of .cat-tabs to padding: 0 16px 12px; (removed top padding) and added bottom padding to .filters-inner

**Checked:** Checked on multiple width by clicking on it. *FIXED*

**Time:** 10 min.
----------------------------------------------------------------------------------------

### C-13: "Veg and Non Veg button does not work properly"

**Reproduced:** 
> clicked on veg btn -> nothing happened
> clicked on non veg -> changed to non veg only
> clicked on veg multiple times -> nothing happened
> refreshed
> clicked on veg multiple times -> changed to veg only

**Thinking Process:**
> Seems random
> but this works perfectly when there are 3 columns
> maybe padding is the issue, clicking padding does nothing I think.

**Cause:**

**Fix:**

**Checked:**

**Time:**
----------------------------------------------------------------------------------------

### C-14: "On mobile devices, filter bar takes half of screen height"

**Reproduced:** went to max-width: 760px media query.

**Thinking Process:** I could make this a dropdown menu, or simply add a filter checkbox that turns off/on the filter bar.

**Cause:** Due to making this filter bar sticky, it takes half of the mobile screen height.

**Fix:** Made an on/off switch for it.

**Checked:** Checked at all the vw. Only at 540px, the filter btn coincides with price slider.
This can be eaily be changed by designer. *FIXED*

**Time:** 30 min
----------------------------------------------------------------------------------------

### C-15: "The filter btn has the arrow-down btn outside (padding area)"

**Reproduced:**

**Thinking Process:**

**Cause:**

**Fix:**

**Checked:**

**Time:**
----------------------------------------------------------------------------------------