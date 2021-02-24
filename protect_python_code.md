Cython : https://en.wikipedia.org/wiki/Cython

Using Cython to protect a Python codebase : https://bucharjan.cz/blog/using-cython-to-protect-a-python-codebase.html

Installing Additional Files : https://docs.python.org/2/distutils/setupscript.html#installing-additional-files


licensing - How do I protect Python code? - Stack Overflow
https://stackoverflow.com/questions/261638/how-do-i-protect-python-code

- Response 1
  - Python, being a byte-code-compiled interpreted language, is very difficult to lock down. Even if you use a exe-packager like py2exe, the layout of the executable is well-known, and the Python byte-codes are well understood.
  - Usually in cases like this, you have to make a tradeoff. How important is it really to protect the code? Are there real secrets in there (such as a key for symmetric encryption of bank transfers), or are you just being paranoid? Choose the language that lets you develop the best product quickest, and be realistic about how valuable your novel ideas are.
  - If you decide you really need to enforce the license check securely, write it as a small C extension so that the license check code can be extra-hard (but not impossible!) to reverse engineer, and leave the bulk of your code in Python.
- Response 2 : Licensing, Web Service 
  - "Is there a good way to handle this problem?" No. Nothing can be protected against reverse engineering. Even the firmware on DVD machines has been reverse engineered and AACS Encryption key exposed. And that's in spite of the DMCA making that a criminal offense.
  - Since no technical method can stop your customers from reading your code, you have to apply ordinary commercial methods.
  - Licenses. Contracts. Terms and Conditions. This still works even when people can read the code. Note that some of your Python-based components may require that you pay fees before you sell software using those components. Also, some open-source licenses prohibit you from concealing the source or origins of that component.
  - Offer significant value. If your stuff is so good -- at a price that is hard to refuse -- there's no incentive to waste time and money reverse engineering anything. Reverse engineering is expensive. Make your product slightly less expensive.
  - Offer upgrades and enhancements that make any reverse engineering a bad idea. When the next release breaks their reverse engineering, there's no point. This can be carried to absurd extremes, but you should offer new features that make the next release more valuable than reverse engineering.
  - Offer customization at rates so attractive that they'd rather pay you do build and support the enhancements.
  - Use a license key which expires. This is cruel, and will give you a bad reputation, but it certainly makes your software stop working.
  - Offer it as a web service. SaaS involves no downloads to customers.
- Response 3 : Python is not the tool, Even Compiled Program can be Reverse-Engineered, Have Legal requirement, SaaS
  - Python is not the tool you need
  - You must use the right tool to do the right thing, and Python was not designed to be obfuscated. It's the contrary; everything is open or easy to reveal or modify in Python because that's the language's philosophy.
  - If you want something you can't see through, look for another tool. This is not a bad thing, it is important that several different tools exist for different usages.
  - Obfuscation is really hard
  - Even compiled programs can be reverse-engineered so don't think that you can fully protect any code. You can analyze obfuscated PHP, break the flash encryption key, etc. Newer versions of Windows are cracked every time.
  - Having a legal requirement is a good way to go
  - You cannot prevent somebody from misusing your code, but you can easily discover if someone does. Therefore, it's just a casual legal issue.
  - Code protection is overrated
  - Nowadays, business models tend to go for selling services instead of products. You cannot copy a service, pirate nor steal it. Maybe it's time to consider to go with the flow...
- Response 4 : Compile python (use Cython) and distribute binaries!
  - Sensible idea:
  - Use Cython, Nuitka, Shed Skin or something similar to compile python to C code, then distribute your app as python binary libraries (pyd) instead.
  - That way, no Python (byte) code is left and you've done any reasonable amount of obscurification anyone (i.e. your employer) could expect from regular Code, I think. (.NET or Java less safe than this case, as that bytecode is not obfuscated and can relatively easily be decompiled into reasonable source.)
  - Cython is getting more and more compatible with CPython, so I think it should work. (I'm actually considering this for our product.. We're already building some thirdparty libs as pyd/dlls, so shipping our own python code as binaries is not a overly big step for us.)
  - See This Blog Post (not by me) for a tutorial on how to do it.  : Compiling your python app with Cython - biicode Blog
    "https://web.archive.org/web/20170602015512/http://blog.biicode.com/bii-internals-compiling-your-python-application-with-cython/ "
- Response 5 : pyminifier : It does Minify, obfuscate, and compress Python code
  - Have you had a look at pyminifier? It does Minify, obfuscate, and compress Python code. The example code looks pretty nasty for casual reverse engineering.
- Response 6 : Do not rely on obfuscation, sign a contract
  - Do not rely on obfuscation. As You have correctly concluded, it offers very limited protection. 
  - woot13-kholia.pdf : UPDATE: Here is a link to paper which reverse engineered obfuscated python code in Dropbox. The approach - opcode remapping is a good barrier, but clearly it can be defeated.
    "https://www.usenix.org/system/files/conference/woot13/woot13-kholia.pdf "
  - Instead, as many posters have mentioned make it:
  - Not worth reverse engineering time (Your software is so good, it makes sense to pay)
  - Make them sign a contract and do a license audit if feasible.
  - Alternatively, as the kick-ass Python IDE WingIDE does: Give away the code. That's right, give the code away and have people come back for upgrades and support.
- Response 7 : Use Cython : This is basically un-reversable, compared to .pyc bytecode!
  - Use Cython. It will compile your modules to high-performant C files, which can then be compiled to native binary libraries. This is basically un-reversable, compared to .pyc bytecode!
  - I've written a detailed article on how to set up Cython for a Python project, check it out:
  - Protecting Python Sources With Cython - Vitaly Gordon - Medium
    "https://medium.com/@xpl/protecting-python-sources-using-cython-dcd940bb188e "
- Response 8 : Use pyconcrete : pyconcrete is an experimental project, there is always a way to decrypt .pye files, but pyconcrete just make it harder.
  - I was surprised in not seeing pyconcrete in any answer. Maybe because it's newer than the question?
  - It could be exactly what you need(ed).
  - Instead of obfuscating the code, it encrypts it and decrypts at load time.
- Response 9 : Use pyprotect
  - GitHub - ga0/pyprotect: A lightweight python code protector, makes your python project harder to reverse engineer
    "https://github.com/ga0/pyprotect "
- Response 10 : Use pyarmor
