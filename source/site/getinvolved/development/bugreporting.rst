
.. _QGIS-bugreporting:

Bugs, Features and Issues
=========================

QGIS is a largely volunteer driven project, and is the work of a dedicated
team of developers, documenters, translators and supporters.
Despite the efforts of the team to release QGIS without bugs, there may remain
some bugs. If you find a bug or want new features to be added, please report it!

Where to report?
----------------

Each part of the QGIS Project has a dedicated place where issues (feature requests
or bugs) can be reported, managed and discussed. Depending on the area you
encountered the issue, the table below indicates the right repository to report it:

================================================== ======================================================
 Place you found the bug or request a feature for   Place to report the issue
================================================== ======================================================
 Applications (QGIS Desktop, QGIS Server)           https://github.com/qgis/QGIS/issues
 QGIS Website (https://qgis.org)                    https://github.com/qgis/QGIS-Website/issues
 QGIS Documentation (https://docs.qgis.org)         https://github.com/qgis/QGIS-Documentation/issues
 C++ API (https://qgis.org/api)                     https://github.com/qgis/QGIS/issues
 PyQGIS API  (https://qgis.org/pyqgis)              https://github.com/qgis/QGIS/issues (for contents) and
                                                    https://github.com/qgis/pyqgis/issues (for formatting)
 External plugins                                   The author repository set in the plugin description
================================================== ======================================================


For help and questions, please contact the :ref:`QGIS-mailinglists`.

Reporting issues on QGIS applications
---------------------------------------

QGIS applications (QGIS Desktop and QGIS Server) issues are available in
`Github <https://github.com/qgis/QGIS/issues>`_.  In order to submit or comment
a report, you need to register and login.


Before reporting an issue
..........................

Before filing an issue, verify that you are running the currently supported
versions |ltrrelease| or |release| or the development version |devversion|
(see also :ref:`QGIS-release-schedule`) and review the currently open issues to
make sure that you aren't creating a duplicate. If you have additional
information on an issue, you can add it to the existing ticket. Third party
plugins might also cause problems.  If you have installed any, you should also
verify that the problem is still reproducible without them.  Please don't
report multiple unrelated bugs
in a single bug report.

When you're are logged in, a ``New Issue`` button is available. Select it and
follow the instructions there.

Before sending the report, please check the formatting of your report by clicking
on "Preview". Please avoid editing existing reports, if not for typos.
Better add further comments in any other case.

Creating a backtrace
^^^^^^^^^^^^^^^^^^^^

If you have a crash it might be useful to include a backtrace as the bug might
be not reproducible on another machine.

On Linux QGIS automatically tries to use ``gdb`` to connect to the crashing
process to produce a backtrace. But some distributions disable the possiblity
to connect debuggers to a running processes. In that case ``gdb`` only
produces a rather useless message like::

 QGIS died on signal 11Could not attach to process.
 If your uid matches the uid of the target process,
 check the setting of /proc/sys/kernel/yama/ptrace_scope, or try
 again as the root user.
 For more details, see /etc/sysctl.d/10-ptrace.conf
 ptrace: Operation not permitted.
 No thread selected
 No stack.
 gdb returned 0
 Aborted (core dumped)

In that case you should reenable that option by setting
``kernel.yama.ptrace_scope`` to 0 in ``/etc/sysctl.d/10-ptrace.conf`` (or
``/etc/sysctl.conf`` or some other file in ``/etc/sysctl.d/``) and
run ``sysctl -p`` as root. When you reproduce the crash after that,
a backtrace will be printed instead.

If you cannot reproduce the crash, there should still be a core dump in the
current directory, that can be analysed after the process has already
terminated. It's called ``core`` (on some systems a dot and the process id is
append to the filename).

On some distributions the creation of core dumps is also disabled. In the
event that you just get ``Aborted`` instead of ``Aborted (core dumped)`` when the
crash occurs. Then you need to run ``ulimit -c unlimited`` before starting QGIS.
You can also include that in your ``.profile``, so that it's always enabled when
you login.

To produce a backtrace from the core file, start ``gdb
/path/to/the/qgis/binary core``. The binary is usually ``/usr/bin/qgis`` or
``/usr/bin/qgis.bin`` on Debian with the GRASS plugin installed. In ``gdb``
you run ``bt`` which will produce the backtrace.

Log output on Windows
^^^^^^^^^^^^^^^^^^^^^^^

The nightly build in OSGeo4W_ (package qgis-dev) is built with debugging
output, that you can view with DebugView_. If the problem is not easy to
reproduce the output might shed some light about where QGIS crashes.


.. _OSGeo4W: https://trac.osgeo.org/osgeo4w
.. _DebugView: https://docs.microsoft.com/en-us/sysinternals/downloads/debugview


Reporting issues on QGIS web site or documentation
---------------------------------------------------

QGIS project provides an active `web site <https://qgis.org>`_ and a rich
`documentation <https://qgis.org/en/docs/index.html>`_. Despite our efforts,
if you find an out of date information, a wrong or unclear statement
or miss a valuable information, please feel free to report it.

The main sources of these documents are hosted and managed in GitHub repositories
so in order to report bugs or submit patches, you need a GitHub account and login.

To get started, first `Create a GitHub account <https://github.com/join>`_.

Then, choose the appropriate repository:

* https://github.com/qgis/QGIS-Documentation/issues for QGIS documentation
* https://github.com/qgis/QGIS-Website/issues for the web site

Check if the issue you'd like to report is not already entered.

Click **New Issue**, type a title and a clear description for your issue.

When you're finished, click **Submit new issue**.

.. note::
  A ``Fix me`` link is provided at the bottom of any page of the web site
  to help you directly improve this page and submit pull request.

  This option is also available in the footer of the documentation.

Reporting plugin issues
-----------------------

Most of the plugins in QGIS are published in the official `QGIS Plugins repository
<https://plugins.qgis.org/plugins/>`_. Bugs or feature requests relative to them
**must** be opened in their respective bug tracking system:

* For any plugin available in QGIS repository, you'll find in its metadata a
  link to its bug tracker. Otherwise, consult the plugin documentation to find
  the address of the relevant bug tracking system or a developer to contact.

  If no information is available, please report it to the `Developer
  mailing-list <https://lists.osgeo.org/mailman/listinfo/qgis-developer>`_.

* For other plugins, we have no means to ensure such information are provided.


Submitting a Patch to QGIS projects
-----------------------------------

In addition to issue report, you can help to fix issues. Fixing issues is done
in GitHub through pull requests. You need to `fork the repository
<https://help.github.com/articles/working-with-forks/>`_ you want to
contribute to and submit pull requests at:

* https://github.com/qgis/QGIS for QGIS Desktop or QGIS Server applications
* https://github.com/qgis/QGIS-Website for the web site at https://qgis.org
* https://github.com/qgis/QGIS-Documentation for the documentation
  available at https://docs.qgis.org

You can find a few guidelines that will help you to easily get your patches
and pull requests into QGIS projects at `submit_patch
<https://docs.qgis.org/testing/en/docs/developers_guide/git.html#submitting-patches-and-pull-requests>`_.
And more widely, You may need to read `git_access
<https://docs.qgis.org/testing/en/docs/developers_guide/git.html>`_.
