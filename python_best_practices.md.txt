## **The Zen of Python Coding philosophy**

1.  Beautiful is better than ugly.
2.  Explicit is better than implicit.
3.  Simple is better than complex.
4.  Complex is better than complicated.
5.  Flat is better than nested.
6.  Sparse is better than dense.
7.  **Readability counts**.
8.  Special cases aren't special enough to break the rules.
9.  Although practicality beats purity.
10. Errors should never pass silently.
11. Unless explicitly silenced.
12. In the face of ambiguity, refuse the temptation to guess.
13. There should be one-- and preferably only one --obvious way to do it.
14. Although that way may not be obvious at first unless you're Dutch.
15. Now is better than never.
16. Although never is often better than *right* now.
17. If the implementation is hard to explain, it's a bad idea.
18. If the implementation is easy to explain, it may be a good idea.
19. Namespaces are one honking great idea -- let's do more of those!

***\**** Guido van Rossum, author of PYTHON programming language, states that code is read much more often than it is written, hence **CODE READABILITY MATTERS**

# PEP 8 Coding Conventions / Best-Practices (**must go-through links**)

-  [*https://www.python.org/dev/peps/pep-0008/*](https://www.python.org/dev/peps/pep-0008/)
-  [*http://docs.python-guide.org/en/latest/wriPEP 8 coding-style conventions / coding best-practices*](http://docs.python-guide.org/en/latest/writing/style/#zen-of-python)
-  [*https://dev.to/j0nimost/setting-up-pep8-and-pylint-on-vs-code-34h*](https://dev.to/j0nimost/setting-up-pep8-and-pylint-on-vs-code-34h)
-  [*https://www.digitalocean.com/community/tutorials/how-to-package-and-distribute-python-applications*](https://www.digitalocean.com/community/tutorials/how-to-package-and-distribute-python-applications)

## CODING BEST PRACTICES

- ### Use a full-fledged IDE such as VSCode or Pycharm with a host of features. Desist from using notepad styled editors.

- ## Source Code Organization

     - **Docstrings** 
     
        - Add docstring with a description of the module’s functions. If the description is long, the first line should be a short summary that makes sense on its own, separated from the rest by a newline. Include docstrings for arguments and its datatype, default values if any. PEP8 convention for docstrings [here](https://www.python.org/dev/peps/pep-0257/)

        - All code, including import statements, should follow the docstring. Otherwise, the docstring will not be recognized by the interpreter, and you will not have access to it in interactive sessions (i.e. through `obj.__doc__`) or when generating documentation with automated tools.

     - **Imports** 
     
        - Import built-in modules first, followed by third-party modules, followed by any changes to the path and your own modules. Especially, additions to the path and names of your modules are likely to change rapidly: keeping them in one place makes them easier to find.

        - Imports should usually be on separate lines:
        ```
        Yes: import os
             import sys

        No:  import sys, os
        ```
        - It's okay to say this though:
        ```from subprocess import Popen, PIPE```

        - Imports are always put at the top of the file, just after any module comments and docstrings, and before
          module globals and constants.

        - Imports should be grouped in the following order:
            a. Standard library imports.
            b. Related third-party imports.
            c. Local application/library specific imports.

        - You should put a blank line between each group of imports.

        - Wildcard imports ( from package import * ) should be avoided, as they make it unclear which names are present
          in the namespace, confusing both readers and many automated tools.
    
        - Don’t use `from module import *`  , instead use from module import Name, Name2, Name3... or possibly import module. This makes it much easier to see name collisions and to replace implementations.
        
     - **`__init__.py` and syspath**
    
        - `_init_.py`* is used by the python interpreter to treat directories as packages. Packages play an important role in avoiding namespace collisions. If you read the section 6.4 Packages from [Python Modules](https://docs.python.org/3/tutorial/modules.html), it helps to prevent directories with a common name from hiding other valid modules that occur later in the search path.

        - Hence, the package mechanism simplifies the task of importing packages. By using an init.py you can also do something like `from package.subpackage import *` which would be difficult or tedious to do if we were to keep appending to `sys.path` (in fact we will have to append all the possible modules).
            
-   ### Logging

    Logging is a means of tracking events that happen when some software runs. The software’s developer adds logging calls to their code to indicate that certain events have occurred. An event is described by a descriptive message which can optionally contain variable data (i.e. data that is potentially different for each occurrence of the event). Events also have an importance which the developer ascribes to the event; the importance can also be called the level or severity.
    
    Logging provides a set of convenience functions for simple logging usage.
    These are `debug()`, `info()`, `warning()`, `error()` and `critical()`. 
    Example:
    ```
    import logging
    logging.warning('Watch out!')  # will print a message to the console
    logging.info('I told you so')  # will not print anything
    ```
    More on logging [here](https://docs.python.org/3/howto/logging.html)
    
-   ### Exception Handling
 
    Even though a statement is syntactily correct, it might throw runtime exceptions when executed.
    [Read the docs for Errors and Exceptions](https://docs.python.org/3/tutorial/errors.html)
    
    *Example 1*
    ```
    if not os.path.isfile(file_path):
        raise(exception)
    ```
    
    *Example 2*
    ```
        import sys
        try:
            f = open('myfile.txt')
            s = f.readline()
            i = int(s.strip())
        except OSError as err:
            print("OS error: {0}".format(err))
        except ValueError:
            print("Could not convert data to an integer.")
        except:
            print("Unexpected error:", sys.exc_info()[0])
            raise
    ```
    
-   ### Remove Unused Code
    - Refrain from adding too many comments in the code that might hamper code logic and understandability. Encapsulate code into smaller reusable modules and call them as needed.
    - Move all hard coded values like local file paths to configs or interact via command line to pass arguments

-   ### Code Commenting

    -   Always update the comments when the code changes. Incorrect comments are far worse than no comments, since they are actively misleading.

    -   Comments should say more than the code itself. Examine your comments carefully: they may indicate that you’d be better off rewriting your code (especially, renaming your variables and getting rid of the comment.) In particular, don’t scatter magic numbers and other constants that have to be explained through your code. It’s far better to use variables whose names are self-documenting, especially if you use the same constant more than once. Remember, it is all about readability. For eg:

        <table>
            <tr>
                <td> Wrong </td> 
                <td> win_size -= 20        # decrement win_size by 20 </td>
              </tr>
              <tr>
                  <td> Ok </td>
                  <td> win_size -= 20        # leave space for the scroll bar </td>
              </tr>
        </table>

    -   Also, think about making constants into class or instance data, since it’s all too common for ‘constants’ to need to change or to be needed in several methods.

    -   Use comments starting with \#, not strings, inside blocks of code. Python ignores real comments, but must allocate storage for strings (which can be a performance disaster inside an inner loop).

    -   Start each method, class and function with a docstring using triple double quotes *"""*. The docstring should start with a 1-line description that makes sense by itself. This should be followed by a blank line, followed by descriptions of the parameters (if any).

    -   Always update the docstring when the code changes. Like outdated comments, outdated docstrings can waste a lot of time.

    -   Finally, add any more detailed information, such as a longer description, notes about the algorithm, detailed notes about the parameters, etc. If there is a usage example, it should appear at the end. Make sure any descriptions of parameters have the correct spelling, case, etc. For eg:
    ```
        def __init__(self, data, name=' ', alphabet=None):

        """Returns new Sequence object with specified data, name, alphabet.

            Arguments:
                - data: The sequence data. Should be a sequence of characters.
                - name: Arbitrary label for the sequence. Should be string-like.
                - alphabet: Set of allowed characters. None by default.
                - Note: if alphabet is None, performs no validation.
        """
    ```

- ### Rule of 30 and Line Length

    - Limit lines to 100 characters.
    - A method should contain less than 40-50 lines of code.
    - A class should contain less than 30 methods.

- ### Whitespace in Expressions and Statements

    - Avoid trailing whitespace anywhere. Because it's usually invisible, it can be confusing. Avoid extraneous
    whitespace in most situations.
    ```
    Yes: spam(ham[1], {eggs: 2})
    No: spam( ham[ 1 ], { eggs: 2 } )

    Yes: foo = (0,)
    No: bar = (0, )

    Yes: if x == 4: print x, y; x, y = y, x
    No: if x == 4 : print x , y ; x , y = y , x
    ```

- ### Return Statements

    - Be consistent in return statements. Either all return statements in a function should return an expression, or
    none of them should. If any return statement returns an expression, any return statements where no value is
    returned should explicitly state this as return None, and an explicit return statement should be present at the
    end of the function (if reachable).
    ```
    Yes:
        def foo(x):
            if x >= 0:
                return math.sqrt(x)
            return None

        def bar(x):
            if x < 0:
                return None
            return math.sqrt(x)

    No:
        def foo(x):
            if x >= 0:
                return math.sqrt(x)

        def bar(x):
            if x < 0:
                return
            return math.sqrt(x)
    ```
- ### Boolean Value Check

    - Don't compare boolean values to True or False using ==.

    ```
    Yes: if greeting:
    No: if greeting == True:
    Worse: if greeting is True:
    ```
    - For sequences, (strings, lists, tuples), use the fact that empty sequences are false.

    ```
    Yes: if not seq:
         if seq:

    No: if len(seq):
        if not len(seq):
    ```
    
- ### Code Coverage

    Coverage.py is a tool for measuring code coverage of Python programs. It monitors your program, noting which parts of the code have been executed, then analyzes the source to identify code that could have been executed but was not. Coverage      measurement is typically used to gauge the effectiveness of tests. More details [here](https://coverage.readthedocs.io/en/coverage-5.1/)
    
- ### Unittest
    
    Python standard library is prebuilt with a module named unittest. Inspired by JUnit and other unit testing frameworks from major programming languages, unittest is a testing framework that lets you automate tests, setup shared setup and shutdown code for tests and more.

    One of the important features of unittest is test fixture, i.e. the setup needed to run one or more tests, and any associated cleanup actions. With text fixture, activities, like creating temporary or proxy databases, directories, or starting a server process, can be taken care of at a single location.

    Let us take few sample test cases and see how they are implemented using unittest:
    ```
        import unittest

        class TestStringMethods(unittest.TestCase):

            def test_upper(self):
                self.assertEqual(‘foo’.upper(), ‘FOO’)

            def test_isupper(self):
                self.assertTrue(‘FOO’.isupper())
                self.assertFalse(‘Foo’.isupper())

            def test_split(self):
                s = ‘hello world’
                self.assertEqual(s.split(), [‘hello’, ‘world’])
                # check that s.split fails when the separator is not a string
                with self.assertRaises(TypeError):
                    s.split(2)

            if __name__ == ‘__main__’:
                unittest.main()
    ```

    Create a test case by subclassing unittest.TestCase. Then you can define individual tests with methods. Note that the test case names should start with the word test. This naming convention informs the test runner about which methods represent tests.

    test runner is the component which orchestrates the execution of tests and provides the outcome to the user. It’s implementation varies and it may use a graphical interface, a textual interface, or return a special value to indicate the results of executing the tests.

-   ### Naming Conventions

    - Avoid using [reserved words](https://docs.python.org/2.5/ref/keywords.html) as variable names. Follow below examples:
        <table>
            <thead>
                <tr>
                     <td> <b>Type</b> </td>
                     <td> <b>Convention</b> </td>
                     <td> <b>Positive Example</b> </td>
                     <td> <b>Negative Example</b> </td>
                </tr>
            </thead>
            <tbody>
               <tr>
                    <td> function</td>
                    <td> verb_with_underscores </td>
                    <td> multiply_by_two </td>
                   <td> db </td>
                </tr>
                <tr>
                    <td> variable</td>
                    <td> noun_with_underscores </td>
                    <td> curr_index </td>
                    <td> type, dict_to_store_defns_of_a_word </td>
                </tr>
                <tr>
                    <td> constant</td>
                    <td> NOUN_ALL_CAPS </td>
                    <td> CLUSTER_SIZE </td>
                    <td> CS </td>
                </tr>
                <tr>
                    <td> class</td>
                    <td> MixedCaseNoun </td>
                    <td> IndexedCorpus </td>
                    <td> Stack</td>
                </tr>
                <tr>
                    <td> public property</td>
                    <td> MixedCaseNoun </td>
                    <td> IsPaired </td>
                    <td> IP </td>
                </tr>
                <tr>
                    <td> private property</td>
                    <td> _noun_with_leading_underscore </td>
                    <td> _is_updated </td>
                    <td> _swap_nums </td>
                </tr>
                <tr>
                    <td> public method</td>
                    <td> mixedCaseExceptFirstWordVerb </td>
                    <td> stripTrailingSpace </td>
                    <td> moveInts </td>
                </tr>
                <tr>
                    <td> private method</td>
                    <td> _verb_with_leading_underscore </td>
                    <td> _check_if_paired </td>
                    <td> _check </td>
                </tr>
                <tr>
                    <td> really private data</td>
                    <td> __two_leading_underscores </td>
                    <td> __delegator_object_ref </td>
                    <td> __obj </td>
                </tr>
                <tr>
                    <td> parameters that match properties</td>
                    <td> SameAsProperty </td>
                    <td> def __init__(data, Alphabet=None) </td>
                    <td> run </td>
                </tr>
                <tr>
                    <td> factory function</td>
                    <td> MixedCase </td>
                    <td> InverseDict </td>
                    <td>  Error</td>
                </tr>
                <tr>
                    <td> module</td>
                    <td> lowercase_with_underscores </td>
                    <td> unit_test </td>
                    <td> UnitTest</td>
                </tr>
                <tr>
                    <td> global variables</td>
                    <td> gMixedCaseWithLeadingG </td>
                    <td> Mixed case prefixed with ‘g’ for globals. Globals should be used extremely rarely and with caution, even if you sneak them in using the Singleton pattern or some similar system. </td>
                    <td> globalVariable</td>
                </tr>
            </tbody>
            </table>
