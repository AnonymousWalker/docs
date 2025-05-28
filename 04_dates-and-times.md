# Dates and Times

All dates use the format (YYYY-MM-DD). All times use the format (hh:mm:ss tt). Date-time values combine the date and the time values with a capital letter `T` (YYYY-MM-DDThh:mm:ss tt). These are a limited subset of the ISO 8601 standard.

### Times

Time values are only permitted for time fields and date-time fields. If a date-time is provided for a date field, an error will result.

### Time Zones

All times are assumed to be in some local time zone. Therefore, no specified time zones (including UTC) are supported. If a time zone is provided in a date-time field (YYYY-MM-DDThh:mm:ssZ), an error will result.