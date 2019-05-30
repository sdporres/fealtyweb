---
layout: none
title: Buildings
section: basics
---

## Overview

Settlements are the population centers on the Kingdom Mode map. Taking control of settlements is central to  the Kingdom Mode because settlements are the only source for Population and Food.

    buildings.Add(new KGBuildingProto
    {
        ID = 1,
        Name = "Manor",
        Description = $"Workers improve the overall efficiency of the Settlement\nIncreases population limit by {FealtyConfig.Instance.ManorPopLimit}",
        Type = BuildingTypes.Manor,
        CoinCost = 500,
        ActionTicks = FealtyDefs.TICKS_IN_A_DAY * 12,
        Unique = true
    });
    buildings.Add(new KGBuildingProto
    {
        ID = 2,
        Name = "Cottage",
        Description = $"Workers increase the Growth of the Settlement\nIncreases population limit by {FealtyConfig.Instance.CottagePopLimit}",
        Type = BuildingTypes.Cottage,
        CoinCost = 175,
        ActionTicks = FealtyDefs.TICKS_IN_A_DAY * 5
    });
    buildings.Add(new KGBuildingProto
    {
        ID = 3,
        Name = "Market",
        Description = $"Workers produce {FealtyConfig.Instance.MarketDailyProduction} Coin daily",
        Type = BuildingTypes.Market,
        CoinCost = 200,
        ActionTicks = FealtyDefs.TICKS_IN_A_DAY * 7
    });







<!-- <span style="color:blue"> blue text</span> -->