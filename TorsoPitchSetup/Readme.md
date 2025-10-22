# Torso pitch setup

⚙️ The torsoPitch setup includes a torso-pitch joint (see XXX documentation) fitted with both an AMO encoder and the existing Aksim encoder to measure joint position. One encoder is used for closed‑loop control and is calibrated; the other serves as an uncalibrated reference for verification. Which encoder the controller uses is defined in the configuration file: the controller encoder is labeled `real` and the secondary encoder `fake` (note that the `fake` encoder is not calibrated). See the configuration section for details on assigning `real` and `fake` encoders.

A dedicated bar allows attaching weights to test the joint's static torque. Because this joint uses the `P1000`, motor temperature can be read via the `TDB_DIFF` board.

![shared image (9)](https://github.com/user-attachments/assets/48443f24-996d-4e82-9fde-2f321736520c)

## BOM 
__Main components__

| Component                        | Rev     | Wingst or cad ref | Note   |
|----------------------------------|---------|-------------------|--------|
| EMS                              | UNKNOWN | 4546              |        |
| 2FOC                             | UNKNOWN | 3336              |        |
| I2C_EXT                          | B       | 18276             |        |
| TDB_DIFF                         | C       | 18570             | PT1000 |
| EMS-EADP                         | A       | 1519              |        |
| AMO                              | B       | 6778              |        |
| AksIM encoder                    |          | 16960            |  AksIM-2™ Off-Axis rotary absolute encoder module, 49mm, 5V, 19 bits per rev, SPI interface       |
| Magnetic wheel for AksIM encoder |         | 16165             | 49mm radius, 2mm thickness |
| Magnetic Encoder for AMO         |         | 10077             |   øe=50.7 øi=44 L=6mm       |




## Configuration files

Configuration files are in: https://github.com/robotology/robots-configuration/blob/devel/experimentalSetups/torso_pitch_mj1_setup. 
For changing the `real`and `fake` encoder, you need to change the `mc_service`. Then you need to arrange the `mec`file for arrange the `gearboxE2J` parameter end the calibration file accordingly.

On the above-mentioned files you can find the instructions on how to make the change.



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


