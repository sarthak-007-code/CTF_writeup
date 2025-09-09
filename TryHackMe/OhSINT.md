# **OhSINT**

### **The Challenge: A Single Image**

The entire challenge revolves around one file: a JPEG image named WindowsXP\_1551719014755.jpg.  
On the surface, it looks like a standard, classic Windows XP background. But as we'll see, the real gold lies not in what the image shows, but in what it *contains*.

### **The OSINT Methodology**

Here is the step-by-step process I followed to solve the challenge.

#### **1\. The Starting Point: Metadata**

My first move was to analyze the image's metadata. This is the low-hanging fruit of OSINT, as many files contain hidden information like creation dates, author names, and even location data. I used the trusty exiftool for this task.  
exiftool WindowsXP\_1551719014755.jpg

The output was a jackpot. The Copyright field revealed a name and an email address: **Copyright OwOdflint@gmail.com**. We now have a solid lead: the username **'OwOdflint'**.

#### **2\. Pivoting to Social Media**

With a username in hand, the next logical step is to see where else this person exists on the internet. A simple search for "OwOdflint" on a search engine led me straight to their Twitter account, @OwOdflint.  
A quick glance at their profile picture confirmed our first answer: their avatar is a **'cat'**.

#### **3\. Geolocation via Wi-Fi**

While browsing their Twitter timeline, I found a tweet where they mentioned their Wi-Fi's BSSID. A BSSID is a unique identifier for a wireless access point, and services like Wigle.net maintain databases that map these IDs to geographical locations.  
I entered the BSSID into the Wigle.net search tool, and it pinpointed the location to **'London'**.

#### **4\. Confirming the Email on GitHub**

I then searched for the username "OwOdflint" on GitHub. Their profile was easily found, and in the profile information, I saw the email address **OwOdflint@gmail.com**, which corroborated the information found in the image's metadata. This also confirmed that the site where the email was found was **GitHub**.

#### **5\. Uncovering Final Clues**

The last two clues were found on a personal blog linked from one of their social media accounts. In a post about their travels, they mentioned a holiday they took to **'New York'**. The post also had some hidden text, which upon inspection, revealed their password: **pennYDropper.\!**.

### **Conclusion**

This challenge is a fantastic example of a realistic OSINT investigation. It shows how even the smallest piece of information—a username buried in an image's metadata—can be the thread you pull to unravel a much larger picture. The process of pivoting from one data point to the next is at the core of any successful OSINT operation.

### **Summary of Answers**

* **User's Avatar:** cat  
* **City:** London  
* **SSID of the WAP:** UnileverWiFi  
* **Personal Email Address:** OwOdflint@gmail.com  
* **Site where email was found:** github  
* **Holiday Location:** New York  
* **Password:** pennYDropper.l