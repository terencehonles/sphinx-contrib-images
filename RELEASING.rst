Releasing sphinxcontrib-images
==============================

1. Test release to TestPyPI

 - Bump version by editing sphinxcontrib/images.py
   e.g. from 0.9.2 to 0.9.3.pre1 (use .pre2 second test release etc.)

 - Trigger `publishing to TestPyPI via the GitHub UI`_

2. Test the TestPyPI-release

 - Make a new virtual environment ``python -m venv venv-0.9.3.pre1``

 - Install the prerelease (see note [1]_)::

   pip install \
       --index-url https://test.pypi.org/simple/ \
       --extra-index-url https://pypi.org/simple \
       sphinxcontrib-images

 - Verify the version installed: ``pip freeze | grep sphinxcontrib-images``

 - Verify the prereleased package can build the package docs in docs/::

   cd docs/
   make html


3. Final test release to TestPyPI: Repeat the previous steps but without .preN
   in the version number, e.g. change 0.9.3.pre1 to 0.9.3

4. Merge, tag, and push the tag to GitHub to trigger a release to PyPI

.. [1] Version 0.9.3.pre1 in setup.py is converted to 0.9.3rc1 in TestPyPI
    so to install a specific version of the prerelese use
    'sphinxcontrib-images==0.9.3rc1' with pip.

    If you release to TestPyPI in this order: 0.9.3.pre1 - 0.9.3.pre2 - 0.9.3
    then you should be able to test all three versions by simply installing the
    package without stating the version since 0.9.3.pre2 > 0.9.3.pre1 and
    0.9.3 > 0.9.3.pre2

.. _publishing to TestPyPI via the GitHub UI: https://github.com/sphinxcontrib/images/actions/workflows/test-publish.yml
