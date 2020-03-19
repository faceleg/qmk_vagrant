1. git clone qmk_firmware and qmk_vagrant as sibling folders
2. cd qmk_vagrant and vagrant up
3. from inside qmk_vagrant's vm, run 
```
vagrant up
vagrant ssh
cd /qmk_firmware
sudo make redox_w:faceleg:avrdude
exit
```

Unplug keyboard and plug back in
