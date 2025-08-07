### 🌐 AWS CloudFront - Simplified Notes

#### What's the big deal with AWS CloudFront?

Imagine you have a website, and you want everyone in the world to see it without any annoying delays. But your website's files are sitting on a server in, say, Virginia. Someone in Australia trying to access your site has to wait for the data to travel all the way across the globe.

**CloudFront** is like a global network of super-fast delivery trucks. It takes a copy of your website and places it in locations all over the world. So, when someone in Australia visits your site, they get the content from a nearby location, making it load almost instantly. It also keeps everything safe and sound.

---

### Step-by-Step: Hosting your website with S3 and CloudFront

This is how you get your website online, fast and secure, without making your storage bucket public for everyone to see.

#### 1. Set up your "storage box" (that's an S3 bucket)

* Go to S3 and **create a new bucket**.
* Give it a unique name.
* The most important part: make sure **"Block all public access" is checked**. This is our secret handshake for security. We'll let CloudFront access it, but no one else.

---

#### 2. Get your storage box ready for a website

* Go into your new bucket, find the **Properties** tab, and scroll down to **Static Website Hosting**.
* **Enable** it and tell it your main page is called `index.html`.
* Don't worry about the URL it gives you—it won't work yet because we locked it down.

---

#### 3. Upload your website files

* Go to the **Objects** tab in your bucket.
* **Upload** all your website files: your `index.html`, any images, CSS files, or JavaScript.
* Your files are now stored securely, waiting for CloudFront to grab them.

---

#### 4. Create your global delivery service (that's CloudFront)

* Go to CloudFront and **Create Distribution**.
* For the "Origin Domain," pick the S3 bucket you just made from the dropdown list. CloudFront will automatically recognize it.
* For "Origin Access," choose **Legacy Access Identities (OAI)**. This is how CloudFront gets permission to enter your secure bucket. It'll even offer to **update the bucket policy** for you, so just say "yes" to that.

---

#### 5. Your website is live!

* Wait a few minutes for CloudFront to set up its global network.
* Once it's deployed, you'll get a special **Distribution Domain Name**. It'll look something like `d12345abcdef.cloudfront.net`.
* Copy that URL, paste it into your browser, and boom—your website is now live, fast, and secure for everyone, everywhere!
