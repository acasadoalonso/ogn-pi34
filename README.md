# ogn-pi34
Script to built an OGN station on a Pi4 (Pi3) based on a fresh Raspbian Buster Lite image and OGN version 0.2.8

## preparation
During the setup process you will be asked to edit (using nano) two files, one of them is `myPlace.conf` for which you should have the following credentials at hand:
- SDR device number (to avoid conflicts if you have multiple SDRs installed)
- SDR frequency correction [ppm] (this can also be measured and mofified accordingly post install if unknown)
```
RF:
{
  Device   = 0;            # Device index for OGN reception. E.g. check "sudo rtl_eeprom -d 0" or "-d 1", ...
  FreqCorr = 0;            # [ppm] "big" R820T sticks have 40-80ppm correction factors, measure it with gsm_scan
}
```
- GPS coordinates and altitude for your OGN station, GeoidSepar needs to be disabled:
```
Position:
{ Latitude   =   +48.0000; # [deg] Antenna coordinates
  Longitude  =    +9.0000; # [deg]
  Altitude   =        100; # [m]   Altitude above sea leavel
  # GeoidSepar =       48; # [m]   Geoid separation: FLARM transmits GPS altitude, APRS uses means Sea level altitude
} ;
```
- APRS name:
```
APRS:
{ Call = "SampleAPRSnameToChange";      # APRS callsign (max. 9 characters)
                                        # Please refer to http://wiki.glidernet.org/receiver-naming-convention
} ;
```

The second file to be edited during the setup process is `rtlsdr-ogn.conf` in which `SampleConfigurationFileNameToChange.conf` needs to be replaced with `myPlace.conf`.

## automatic setup
```
sudo apt update
sudo apt install git -y
git clone https://github.com/VirusPilot/ogn-pi34.git
./ogn-pi34/install-pi3.sh # for Pi3
./ogn-pi34/install-pi4.sh # for Pi4
```
## change from Ethernet to WiFi connection
```
sudo raspi-config
```
## post install modifications
### GSM gain/frequency and ppm calibration
- see https://github.com/glidernet/ogn-rf/blob/6d6cd8a15a5fbff122542401180ea7e58af9ed92/INSTALL#L42
### OGN gain
- tbd.
