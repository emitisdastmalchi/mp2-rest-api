# MP2-rest-api

MP2 is a FastAPI app that turns the pipeline from MP1 into a REST API. Users can upload a CSV, view it, and clean it by sending HTTP requests, rather than running the pipleline as a script.

## Endpoints:
- `GET /health` checks that the server is running and returns the API version.
- `POST /upload` accepts a CSV file, stores it in memory under a new ID, and returns its filename, row count, and column names.
- `GET /datasets/{id}` returns up to `limit` rows from a stored dataset, along with its total number of rows.
- `POST /datasets/{id}/process` validates and cleans a stored dataset using the MP1 functions (removing invalid values -- data_validator, duplicates, and missing data -- data_processor), saves the cleaned version, and returns a cleaning report.

## Other Features:

- **Middleware** logs every request with a unique request ID, the status code, and how long it took.
- **Error handling** returns clear status codes: 400 for bad uploads or invalid settings, 404 for datasets that don't exist, and 422 for bad requests.
- **Tests** written with pytest check uploading, processing, and retrieving data.

## Run:

```bash
python -m pip install -r requirements.txt
python -m uvicorn main:app --reload
```

Then open http://127.0.0.1:8000/docs to try the endpoints.

To run the tests:

```bash
python -m pytest tests -v
```