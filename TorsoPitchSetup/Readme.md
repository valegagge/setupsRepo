The torsoPitch setup is composed by a torsopitch joint (BOM to be completed) with the addiction of e AMO encoder and a bar where put weights.


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
