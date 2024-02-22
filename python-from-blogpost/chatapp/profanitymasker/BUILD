python_sources(
    name="lib"
    dependencies=[":bad_words"]
)

python_tests(
    name="tests",
)

resource(
    name="bad_words",
    source="bad_words.json"
)


# This target allows you to build a `.whl` bdist and a 
# `.tar.gz` sdist by auto-generating
#  `setup.py`. See https://www.pantsbuild.org/docs/python-distributions.
#
# Because this target has no source code, Pants cannot infer dependencies.
# It depends on `:lib`,
#  which means it will include all the non-test Python files in this 
# directory and any of
#  their dependencies.
python_distribution(
    name="dist",
    dependencies=[":lib"],
    wheel=True,
    sdist=True,
    provides=setup_py(
        name="chatapp.profanitymasker",
        version="0.0.1",
        description="A profanity masker.",
    ),
)

