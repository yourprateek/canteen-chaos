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

**Checked:** The menu-cards are visible even at 160px width or below!

**Time:** 10 - 15 min  *Found a bug at 490px width EXTRA?*
----------------------------------------------------------------------------------------

### CC-04: "The buttons don't work on my tablet"

**Reproduced:**

**Thinking Process:**

**Cause:**

**Fix:**

**Checked:**

**Time:**
----------------------------------------------------------------------------------------