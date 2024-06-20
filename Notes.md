develop:


-- Docs: https://docs.pytest.org/en/stable/how-to/capture-warnings.html
==================================================== short test summary info ====================================================
FAILED tests/test_upload_svg.py::test_svg_upload_sanitize - assert 500 == 201
FAILED tests/test_upload_svg.py::test_svg_upload_invalid_format - assert 500 == 201
FAILED tests/data_manager/api_tasks.tavern.yml::tasks-storage-filename-local
============================= 3 failed, 544 passed, 78 skipped, 26530 warnings in 223.18s (0:03:43)

my branch man/friend:
FAILED tests/test_endpoints.py::test_urls_mismatch_with_registered - AssertionError: URL name mismatch found. If you created, removed or updated URLs, run the following command:
FAILED tests/test_upload_svg.py::test_svg_upload_sanitize - assert 500 == 201
FAILED tests/test_upload_svg.py::test_svg_upload_invalid_format - assert 500 == 201
FAILED tests/io_storages_presign_proxy.tavern.yml::get_import_export_storage_types
FAILED tests/data_manager/api_tasks.tavern.yml::tasks-storage-filename-local


(Pdb) context
{'resolve_uri': True, 'request': <rest_framework.request.Request: GET '/api/tasks/?fields=all&view=1'>, 'project': <Project: Test Draft 1 (id=1)>, 'drafts': True, 'predictions': True, 'annotations': True}