objdump -s -j .rodata check

check:     file format elf64-x86-64

Contents of section .rodata:
 2000 01000200 434f5252 4543540a 466c6167  ....CORRECT.Flag
 2010 3a202573 0a005752 4f4e4700 00000000  : %s..WRONG.....
 2020 ffc6a5e2 00000000 00000000 00000000  ................
 2030 00000000 00000000 00000000 00000000  ................
 2040 8df69596 84ac918c 8ab5fa8f 8ab29196  ................
 2050 cca2fad1 c7a5c681 c6fe91d0 c7f590da  ................
 2060 cba7c0d0 99f091da caf5c49f     

objdump -s -j .rodata validator

validator:     file format elf64-x86-64

Contents of section .rodata:
 2000 01000200 56414c49 4400466f 726d756c  ....VALID.Formul
 2010 61207665 72696669 65643a20 25730a00  a verified: %s..
 2020 72303074 7b000000 5375626d 69742074  r00t{...Submit t
 2030 6f202e2f 63686563 6b20666f 72206f66  o ./check for of
 2040 66696369 616c2073 636f7269 6e672e00  ficial scoring..
 2050 494e5641 4c494420 2d20666f 726d756c  INVALID - formul
 2060 61206d69 736d6174 63682e20 52656368  a mismatch. Rech
 2070 65636b20 796f7572 20696d70 6c656d65  eck your impleme
 2080 6e746174 696f6e2e 00000000 00000000  ntation.........
 2090 494e5641 4c494420 2d20756e 7265636f  INVALID - unreco
 20a0 676e6973 65642066 6f726d61 742e0000  gnised format...
 20b0 00000000 00000000 00000000 00000000  ................
 20c0 dec0adbe 00000000 00000000 00000000  ................
 20d0 00000000 00000000 00000000 00000000  ................
 20e0 acf09dca a5aa99d0 abb3f28d bcf7cf8d  ................
 20f0 e9a69bdc e9a19c8e efa4958b edf49b89  ................
 2100 ebf0cec3                             ....      


python3 - <<'PY'
def decode(data_hex, key_hex):
    data = bytes.fromhex(data_hex)
    key = bytes.fromhex(key_hex)
    return bytes(b ^ key[i % len(key)]
                 for i, b in enumerate(data))

validator_data = (
    "acf09dcaa5aa99d0abb3f28dbcf7cf8d"
    "e9a69bdce9a19c8eefa4958bedf49b89"
    "ebf0cec3"
)

checker_data = (
    "8df6959684ac918c8ab5fa8f8ab29196"
    "cca2fad1c7a5c681c6fe91d0c7f590da"
    "cba7c0d099f091dacaf5c49f"
)

print("Validator:", decode(validator_data, "dec0adbe").decode())
print("Checker:  ", decode(checker_data, "ffc6a5e2").decode())
PY