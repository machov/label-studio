
test_name: get_import_export_storage_types
test_name: test_empty_storage_list
test_name: test_import_from_azure_storage
test_name: test_export_azure_storage
test_name: test_resolving_embedded_links
test_name: test_import_jsons_from_s3_and_resolve_hypertext
test_name: test_import_jsons_from_s3_and_resolve_partially_encoded
test_name: test_import_json_with_unexisted_s3_links


test_name: get_import_export_storage_types
test_name: test_export_s3_storage
test_name: test_export_s3_storage_with_sse
test_name: test_export_s3_storage_with_kms
test_name: test_export_gcs_storage
test_name: test_empty_storage_list
test_name: test_validate_s3_connection
test_name: test_import_from_azure_storage
test_name: test_export_azure_storage
test_name: test_import_jsons_from_s3
test_name: test_resolving_embedded_links
test_name: test_import_jsons_from_s3_and_resolve_hypertext
test_name: test_import_json_with_unexisted_s3_links
test_name: test_connection_to_import_redis_storage


TODO: edit:
from io_storages.azure_blob.models import AzureBlobImportStorage, AzureBlobImportStorageLink
from io_storages.azure_blob import models


modify:
@contextmanager
def azure_client_mock():
    from collections import namedtuple

    from io_storages.azure_blob import models

    File = namedtuple('File', ['name'])

    class DummyAzureBlob:
        def __init__(self, container_name, key):
            self.key = key
            self.container_name = container_name

        def download_as_string(self):
            return f'test_blob_{self.key}'

        def upload_blob(self, string, overwrite):
            print(f'String {string} uploaded to bucket {self.container_name}')

        def generate_signed_url(self, **kwargs):
            return f'https://storage.googleapis.com/{self.container_name}/{self.key}'

        def content_as_text(self):
            return json.dumps({'str_field': str(self.key), 'int_field': 123, 'dict_field': {'one': 'wow', 'two': 456}})

    class DummyAzureContainer:
        def __init__(self, container_name, **kwargs):
            self.name = container_name

        def list_blobs(self, name_starts_with):
            return [File('abc'), File('def'), File('ghi')]

        def get_blob_client(self, key):
            return DummyAzureBlob(self.name, key)

        def get_container_properties(self, **kwargs):
            return SimpleNamespace(
                name='test-container',
                last_modified='2022-01-01 01:01:01',
                etag='test-etag',
                lease='test-lease',
                public_access='public',
                has_immutability_policy=True,
                has_legal_hold=True,
                immutable_storage_with_versioning_enabled=True,
                metadata={'key': 'value'},
                encryption_scope='test-scope',
                deleted=False,
                version='1.0.0',
            )

        def download_blob(self, key):
            return DummyAzureBlob(self.name, key)

    class DummyAzureClient:
        def get_container_client(self, container_name):
            return DummyAzureContainer(container_name)

    # def dummy_generate_blob_sas(*args, **kwargs):
    #     return 'token'

    with mock.patch.object(models.BlobServiceClient, 'from_connection_string', return_value=DummyAzureClient()):
        with mock.patch.object(models, 'generate_blob_sas', return_value='token'):
            yield



