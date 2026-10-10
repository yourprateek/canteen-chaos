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

**Checked:** The suggestions now appear above the bar. FIXED

**Time:** about 4-5 min.
----------------------------------------------------------------------------------------

### CC-02: "Can't read anything in dark mode"

**Reproduced:** Don't need to reproduce, the name of the dish and its price is another dark color on a darker background.

**Thinking Process:** Seems like a var(--muted) problem. Searched --muted & name-btn(using inspect in browser) in css file. inspected style of name-btn.

**Cause:** color of the name-btn was being inherited by its parent body named dish-body on 293 line.

**Fic:** Deleted color attribute.

**Checked:** Save & refreshed the css file and browser. FIXED

**Time:** about 5-7 min.
----------------------------------------------------------------------------------------

### CC-03: "The menu is wider than my phone"

**Reproduced:** Used Toggle device emulation tool in inspect in edge. Something breaks after shrinking the width past 350px.

**Thinking Process:** maybe there is a media query for this made intentionally, nope. min-width of these card might be 350px, nope. img-wrap's img may have some width issue, I couldn't find any width property that would cause this, though it might not be 350 but 368px = 23rem, nope. Couldn't find anything, I am making another media query specifically for this.

**Cause:** No fallback for menu-cards after reducing width below 350-360px.

**Fix:** made width of menu-card 90% of the viewport width. Also made padding 5% of viewport width so that it stays at center.

**Checked:** The menu-cards are visible even at 160px width or below! FIXED

**Time:** 10 - 15 min  *Found a bug at 490px width EXTRA?*
----------------------------------------------------------------------------------------

### CC-04: "The buttons don't work on my tablet"

**Reproduced:** changed width to 768px for tablet width.This behaviour is for 760px - 900px width.

**Cause:** There is an after element that is above btn thus preventing its interaction.

**Fix:** Deleted the media query responsible for this on line 1031 to 1046

**Checked:** Button was already working lol, now user can interact with it directly. FIXED

**Time:** 2 min
----------------------------------------------------------------------------------------

### CC-05: "The category bar scrolls away on my phone"

**Reproduced:** shifted to 320px width.

**Thinking Process:** something to do with 'sticky position'. sticky is applied to filter. Its parent has overflow-x. Found it.

We want filters div to stick below the .slot-bar div. But that will make the filter tab take up half of the screen on smaller devices.

**Cause:** Overflow property makes the sticky element stick to it not the page.

**Fix:** Deleted the overflow property for it.

**Checked:** It does stick, but it sticks to the top. I dont think this is the actual fix, I'll ask a senior
PENDING

**Time:** >1hr
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

**Checked:** checked on two items that had low badge acive. FIXED

**Time:** about ~4hr
----------------------------------------------------------------------------------------

### CC-07: "Cancelling makes it worse"

**Reproduced:** 

**Thinking Process:**

**Cause:**

**Fix:**

**Checked:**

**Time:**
----------------------------------------------------------------------------------------