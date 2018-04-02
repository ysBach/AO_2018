Written by Yoonsoo P. Bach

2018-04-02



This is a short note to future TAs who will take responsibility of taking care of Astronomical Observation 1 and 2 courses at Seoul National University. 

## Language

TA lecture's language must follow the official language written in the syllabus unless a special necessity is overwhelming. I understand at our department, there are only two possible cases, i.e., Korean lecture and English lecture. In the former case, I think the professor may ask TA to use English if the TA is not a Korean. In the latter case, many TA's tend to use Korean in the TA sessions, without proper notices.

I think the only official reason to change the class language from English to Korean is when the following two are satisfied at the same time:

1. All the students are using Korean more comfortably than English.
2. All the students anonymously wants Korean lecture.

Otherwise, unless professor explicitly asked to, TA must use English in the lecture notes and lectures.

## Computer Practice

I am currently not sure how the computer practice session will change over time. But in 2016, 2017, and 2018, I have done the following things before the first TA practice session began:

1. Download Anaconda3 installation file (for Ubuntu, ``Anaconda3~~~.sh``) and copy it to all the computers
   * I used USB stick to save downloading time.
   * Use the administrator account (It was ``astro-xx`` when I am doing TA works)
   * While doing so, I had to delete the previous ``~/Anaconda3`` directory.
   * Also delete the lines added by previous Anaconda installation in ``~/.bashrc`` file. Usually the last 2 lines.
   * Also I deleted redundant Ubuntu accounts (settings -> Accounts -> click ``unlock`` button at the top-right corner, and delete useless accounts)
   * IMPORTANT: Since the computers are 64-bit, install ``sudo apt-get install gcc-multilib``.
2. Call students to an extra session (not necessarily the class time) to let them learn the following things:
   1. Installation of **Anaconda3** on Ubuntu (PC Room)
   2. Installation of **IRAF/PyRAF** on that computer
   3. Install **Slack** on that computer (Join our workspace if you haven't yet!!!)
      * I recommend to install slack on students' phones too.
   4. While IRAF/PyRAF installation is going on, try `spyder` and basic **python.**
      * The TA may use Jupyter Notebook.
      * Think Python ch 1-3, 5-8, 10-12. (15-17 are optional)
      * SciPy Lecture Note section 1.2.1-4, 1.3.1-4, 1.4.1-2 (1.4.3-7 are optional), 1.5.2, 1.5.5
   5. Run PyRAF and test it with **sample FITS files** provided by the TA.
      * I provided HR30 fits files.
3. Make GitHub account, try `SNUAO_Scratch` repo.
   * The repo is [here](https://github.com/ysBach/SNUAO_Scratch). This repo will be there almost permanently so that all the students who finished AO classes would have taken a look at it at least once. 

## Observations

Observations must be primarily led by the instrumentation TA (It was Ki-Hyun Kim until 2016 and then Jin-Guk Seo from 2017). But the AO course TA must take an important role in the observation too. The TA must do

1. Translate materials in English and hand it to students as much as possible
2. Be there when students are conducting observations. The instrumentation TA is just like a telescope operator, and you must be like a PI.
3. Struggle with students to get observational data to achieve certain project goals you/students/professor(s) have set.
4. Although professor is the most responsible person, TA also must take some part of responsibility when some accidents occur. This is sensitive issue, but please keep in mind you are not a student.
5. ​