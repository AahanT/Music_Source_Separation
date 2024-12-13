import nussl
import os

def bgfgSep(fileDir: str):
    """
    Separate background and foregound of the music and store it as background.wav and foreground.wav

    Args:
        fileDir (str): the path to the file directory 
    """

    directory = os.path.dirname(fileDir)
    bg_file = os.path.join(directory, 'background.wav')
    fg_file = os.path.join(directory, 'foreground.wav')

    if os.path.exists(fileDir):
        try:
            audio_signal = nussl.AudioSignal(fileDir)
            ft2d = nussl.separation.primitive.FT2D(
                audio_signal, mask_type='binary', mask_threshold=0.99, high_pass_cutoff=50, use_bg_2dft=False)
            
            estimates = ft2d()
            background = estimates[0]
            foreground = estimates[1]

            background.write_audio_to_file(bg_file, background.sample_rate)
            foreground.write_audio_to_file(fg_file, foreground.sample_rate)

            return f"Background and Foreground Separated"
        
        except:
            return f"An Error Occured while Separating"
        
    else:
        return f"Input file '{fileDir}' not found."
    


