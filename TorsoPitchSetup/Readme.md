# Torso pitch setup

⚙️ The torsoPitch setup consists of a torso pitch joint (see XXX documentation) equipped with an AMO encoder used to measure the joint position, together with the existing Aksim encoder.
In addition, a dedicated bar allows the placement of weights to test the static torque of the joint.
This joint is equipped with the P1000, so it is possible to read the motor temperature by the TDB_DIFF board.


## BOM 
__Main components__

| Component | Rev     | Wingst or cad ref | Note   |
|-----------|---------|-------------------|--------|
| EMS       | UNKNOWN | 4546              |        |
| 2FOC      | UNKNOWN | 3336              |        |
| I2C_EXT   | B       | 18276             |        |
| TDB_DIFF  | C       | 18570             | PT1000 |
|           |         |                   |        |





## Configuration files

Configuration files are in: https://github.com/robotology/robots-configuration/blob/devel/experimentalSetups/torso_pitch_mj1_setup. 

![shared image (9)](https://github.com/user-attachments/assets/48443f24-996d-4e82-9fde-2f321736520c)

## Connections

``` mermaid
flowchart TD
 subgraph EMS_Board["EMS Board"]
    EMS_P4["P4<br>"]
    EMS_P6["P6<br>"]
    EMS_P9["P9<br>"]
  end
 subgraph TwoFOC["2FOC"]
        FOC_P3["P3<br>"]
        FOC_P5["P5<br>"]
        FOC_P6["P6<br>"]
  end

subgraph Encoder_aksim["Encoder Aksim"]
  end

subgraph Encoder_amo["Encoder AMO"]
  end

subgraph Encoder_mrie["Encoder MRIE"]
  end

subgraph i2c_ext["I2C_EXT"]
  end

subgraph tdb_ext["TDB_EXT"]
  end

EMS_P4 -- CAN --- FOC_P3
EMS_P6 -- SPI --- Encoder_aksim
EMS_P9 -- SPI --- Encoder_amo
FOC_P5 -- ABI --- Encoder_mrie
FOC_P6 -- I2C --- i2c_ext
i2c_ext -- I2C --- tdb_ext



```

