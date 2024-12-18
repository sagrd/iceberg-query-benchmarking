# Simple Table (Not Partitioned)

#### Simple Query
`SELECT Country, Network, AVG(averageSignal) AS AvgSignal FROM nessie.towers_schema.asia_towers GROUP BY Country, Network;`

#### Complex Query
`WITH AverageSignal AS (
    SELECT
        Country,
        Network,
        AVG(averageSignal) AS AvgSignal
    FROM nessie.towers_schema.asia_towers
    GROUP BY Country, Network
),
UniqueUnits AS (
    SELECT
        Country,
        Network,
        COUNT(DISTINCT unit) AS UniqueUnitCount
    FROM nessie.towers_schema.asia_towers
    GROUP BY Country, Network
),
RangeStats AS (
    SELECT
        Country,
        Network,
        MAX(RANGE) AS MaxRange,
        MIN(RANGE) AS MinRange,
        AVG(RANGE) AS AvgRange
    FROM nessie.towers_schema.asia_towers
    GROUP BY Country, Network
)
SELECT
    a.Country,
    a.Network,
    a.AvgSignal,
    u.UniqueUnitCount,
    r.MaxRange,
    r.MinRange,
    r.AvgRange
FROM AverageSignal a
JOIN UniqueUnits u ON a.Country = u.Country AND a.Network = u.Network
JOIN RangeStats r ON a.Country = r.Country AND a.Network = r.Network
ORDER BY a.Country, a.Network;`


# Partitioned Table

#### Simple Query
`SELECT Country, Network, AVG(averageSignal) AS AvgSignal FROM nessie.towers_schema.asia_towers_partitioned GROUP BY Country, Network;`

#### Complex Query
`WITH AverageSignal AS (
    SELECT
        Country,
        Network,
        AVG(averageSignal) AS AvgSignal
    FROM nessie.towers_schema.asia_towers_partitioned
    GROUP BY Country, Network
),
UniqueUnits AS (
    SELECT
        Country,
        Network,
        COUNT(DISTINCT unit) AS UniqueUnitCount
    FROM nessie.towers_schema.asia_towers
    GROUP BY Country, Network
),
RangeStats AS (
    SELECT
        Country,
        Network,
        MAX(RANGE) AS MaxRange,
        MIN(RANGE) AS MinRange,
        AVG(RANGE) AS AvgRange
    FROM nessie.towers_schema.asia_towers
    GROUP BY Country, Network
)
SELECT
    a.Country,
    a.Network,
    a.AvgSignal,
    u.UniqueUnitCount,
    r.MaxRange,
    r.MinRange,
    r.AvgRange
FROM AverageSignal a
JOIN UniqueUnits u ON a.Country = u.Country AND a.Network = u.Network
JOIN RangeStats r ON a.Country = r.Country AND a.Network = r.Network
ORDER BY a.Country, a.Network;`
