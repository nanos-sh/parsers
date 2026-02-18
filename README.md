# NanoSIEM Community Parsers

A collection of VRL parsers for NanoSIEM log source ingestion.

## Structure

Each parser lives in its own directory under `parsers/` with a `parser.yaml` file containing:

- **name**: Machine-readable identifier (snake_case)
- **display_name**: Human-friendly name
- **version**: Semantic version
- **description**: What this parser does
- **category**: Log category (e.g., application, cloud, endpoint, network, security)
- **vendor**: Vendor/organization name
- **product**: Product name
- **parser_vrl**: The VRL transformation code

## Usage

Import these parsers into NanoSIEM via **Log Sources > Repositories**. Parsers are imported as draft log sources ready for review and deployment.

## Contributing

1. Create a new directory under `parsers/` with your parser name
2. Add a `parser.yaml` following the format above
3. Test your VRL in NanoSIEM's parser editor before submitting
