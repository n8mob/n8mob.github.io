---
layout: post
title: "Deploy Early, Regret Often - My Résumé Workflow Odyssey"
categories:
  - career
  - résumé
  - job-search
---

When I started preparing my résumé for my second wave of jobs after college times, I thought that a web-based résumé would be perfect. It would be modern, elegant, and accessible. I expected people to actually view my résumé on their phone. 

I'm sorry, you want a PDF? Why? So you can *print it?* Are you going to take a stack of these to your recruiting retreat, settle down by the fire, and sip hot chocolate while you look over applicant résumés? I'm applying for software-engineering positions—web developer even.

## Phase 1: Markdown + GitHub Pages

My first solution was a clean Markdown file, auto-deployed by GitHub Pages. Simple, version-controlled, and looked great on a phone. And if someone insisted on a PDF, I'd tell them to just print it from the web page. I had a custom print stylesheet, so you wouldn't have to waste paper on my giant section headings.

But it seemed like everyone wanted a PDF.

And so began the *workflow*.

### The Ritual:

1. Edit the Markdown
2. Commit and push to GitHub
3. Wait for the GitHub Pages build to deploy
4. Visit the site, print to PDF
5. Commit the PDF and push *again*
6. Wait for that to publish
7. Send someone a link
8. Hear back: "Can you just send it as an attachment?"

## Phase 2: org-mode (Briefly) + CSS Magic

Eventually, I tried moving to `org-mode` for more structure. I liked having metadata, internal links, collapsible trees. I kept my print stylesheet. The idea was to export to HTML, open that page in a browser, and print to PDF from there.

But that lasted... maybe one revision.

Because after exporting, I had to manually open the file, print the PDF, and then delete the HTML file—which would never be opened again—so it didn't get committed to my repo. It added even more steps for very little gain. The org-mode workflow quietly bowed out.

## Phase 3: Surrender via Apple Pages

I finally decided to stop  trying to convince everyone that it made more sense to go get my latest resume on nategrigg.com/resume.html (or resume.pdf).  And with help from lots of online articles and YouTube videos. (Shout out to Andy LaCivita), I learned that the resume has two basic purposes:

1. It contains a short overview of my career and skills. But the information is secondary, really it's just my token on the game board. A handle to me as an applicant.
2. More importantly, it is a tool to get me into an interview. Probably after a phone screen with a recruiter.

Now that I had stopped trying to make the resume a complete and accurate representation of me as a professional, I was less worried about what might get left out. All that it needed to do was to represent that I had the skills to do a job so that they would talk to me about it.

I'm still sore from cutting some of my favorite stories and accomplishments. But I just have to remember that nobody is going to hire me based on my resume. It only needs to get me the interview.

In that context, the evergreen advice to tailor my resume for (almost) every single application makes a lot more sense! If I'm applying for a job where a particular achievement is going to impress a hiring manager and get me an interview, I put it back in.

A few years ago, I would have used Microsoft Word because it was quite powerful and I was familiar enough with it from work. But a few years back I realized that I was using Office maybe once every other month. So I  cancelled my subscription to Microsoft Office. Google docs was super simple, but if you actually want your document to look like anything besides a Google doc, it's going to be major painful.

I had kept Apple's Pages app on my Mac ever since I tried it on the first iPad back in 2010. (With that first iPad I had bought an upright dock and a Bluetooth keyboard, imagining this was the computer of the future... it was and it wasn't... totally off topic, get it together!) For such an Apple fan-boy, I had used very few Apple applications. And can you blame me? iTunes was... fine... most of the time... XCode? What the... what? But I really liked the way Numbers made "documents" rather than "spreadsheets". So, I figured that if I got "locked in" to this app for my résumé, it wouldn't be the end of the world. The app was free with my Mac.

So, I rebuilt the style of a .pages document  to match the look of my web version. (People don't expect beautiful documents from software engineers, but I'm not going to give them something intentionally ugly!)

Pages has a decent "styles" feature, which was a killer feature for Office back when I really started using it. It's actually a nice transition from CSS. You define "a style", then you can update it everywhere in the document without manually stepping through every heading and making the same tweak over and over. (And forget to update one in the middle, of course.) I still get mad when some cow-orker wants to collaborate on  .docx and they've created their own headings by just selecting the text and changing the font.

So, now I can just look at yesterday's version while going over the job description.  Any stories that don't matter can be removed without remorse. If a story is particularly relevant to a job, I can add the bullet back in and hope they ask me about it. *In the interview.*

## Lessons Learned

- **Automation is great—until you're debugging your layout in production**
- **Git is not a design tool (unless you're very patient)**
- **People still just want attachments, it's that token thing.**
- **They invented \*\*\*\* drag-and-drop WYSIWYG for good reason!**

## Final Thoughts

I still love the idea of a living résumé. But for now? I keep a `.pages` file, a current PDF, and a few +markdown+ org-mode notes.

And maybe one day... I’ll make Résumé Engine 2.0.

> “Can you just send it as an attachment?” – Every recruiter ever
