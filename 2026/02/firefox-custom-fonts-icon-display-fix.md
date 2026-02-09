**Issue: Website Icons Display Incorrectly After Custom Font Setup in Firefox**

**Solution:**  
Go to `about:config` in Firefox, find the preference `browser.display.use_document_fonts.icon_font_allowlist`, and add the specific icon font names used by the affected websites to this allowlist.

**Icon Font Names for Specific Sites:**

*   **Outlook Web App:**  
    `FluentSystemIcons`, `FluentSystemIcons-Regular`, `FluentSystemIcons-Resizable`
*   **Google Services (e.g., Gmail, Drive):**  
    `Google Symbols Subset Subset`

> **Side Note:** The Google font name containing two consecutive "Subset" strings looked like a typo and caused some confusion during troubleshooting.
