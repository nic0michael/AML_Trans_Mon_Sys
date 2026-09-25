# Transaction Generator

The Transaction Generator creates synthetic transaction records for the AML Transaction Monitoring System.

The generator is configured using `config.yaml`.

## Configuration

Example:

```yaml
number_of_records: 20

record_type: GOOD_RECORDS

fraud_percentage: 0
```

### `number_of_records`

Specifies the total number of transaction records to generate.

Example:

```yaml
number_of_records: 20
```

This generates 20 transaction records.

### `record_type`

Controls the type of transaction data generated.

#### Good records

```yaml
record_type: GOOD_RECORDS
```

Use this when generating normal transactions without intentionally generated fraud activity.

For good records, set:

```yaml
fraud_percentage: 0
```

#### Records with fraud

```yaml
record_type: RECORDS_WITH_FRAUD
```

Use this when generating a mixture of normal and fraudulent transactions.

Example:

```yaml
number_of_records: 20
record_type: RECORDS_WITH_FRAUD
fraud_percentage: 10
```

This requests 20 records with approximately 10% representing fraudulent activity.

That results in:

```text
Total records : 20
Fraud records  : 2
Good records   : 18
```

Another example:

```yaml
number_of_records: 100
record_type: RECORDS_WITH_FRAUD
fraud_percentage: 25
```

Results in:

```text
Total records : 100
Fraud records  : 25
Good records   : 75
```

## Configuration Rules

`number_of_records` must be greater than zero.

`fraud_percentage` must be between `0` and `100`.

For:

```yaml
record_type: GOOD_RECORDS
```

use:

```yaml
fraud_percentage: 0
```

For:

```yaml
record_type: RECORDS_WITH_FRAUD
```

the `fraud_percentage` determines the proportion of generated records that contain intentionally generated fraud activity.

## Configuration File Location

The application expects:

```text
config.yaml
```

in the application's working directory.

Example:

```text
transaction-generator/
├── config.yaml
├── README.md
└── ...
```

## Example Configurations

### Generate only good records

```yaml
number_of_records: 100
record_type: GOOD_RECORDS
fraud_percentage: 0
```

### Generate 10% fraud records

```yaml
number_of_records: 100
record_type: RECORDS_WITH_FRAUD
fraud_percentage: 10
```

### Generate 25% fraud records

```yaml
number_of_records: 1000
record_type: RECORDS_WITH_FRAUD
fraud_percentage: 25
```


