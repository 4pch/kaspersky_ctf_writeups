# Writeup 1

Author's solution for Sleepy Cucumber 

We’re given a serialized neural network hidden inside a dill pickle, compressed with gzip. After installing dill and unpacking the file, we can load the object into Python. Once loaded, a quick look at its attributes shows four private fields (_enc_flag, _model, _trigger_len, _vec) and a method called predict. That’s our main point of interest.

Since we don’t have the original source code, the next move is to disassemble the predict function. Inspecting the bytecode reveals what the method is doing. It takes the first layer’s weights (self.model.coefs[0]), flattens them, and reinterprets them as 64-bit integers. From each of these integers, it extracts just the least significant bit. The number of bits to extract is given by self._trigger_len. These bits are then grouped into bytes, which are turned into ASCII characters. This forms the hidden trigger string.

So, to reconstruct the trigger, we just mimic that logic: flatten the first layer’s weights, cast them to uint64, grab the lowest bit of each element, and rebuild the string byte by byte. Doing this reveals the secret trigger embedded inside the model.

The last step is simple: pass this trigger into the predict method. The model then uses it to decrypt the hidden flag (via SHA-256 and XOR, as hinted by the disassembly). The output is a flag: kaspersky{n0t_4ll_cucumb3r5_4r3_equ4lly_g00d_f0r_y0u}
