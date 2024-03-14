Takes advantage of Raw input buffer, injects into obs - creates a local website on with localhost url for configuring settings such as delay. Does log HWID (unsure what else it logs) 
The log.txt file added in the github contains logs of different versions of the loader, the log shows what api calls were made to the system during the code - as you can see they remain consistent regardless of file size (changed by bloat code) and then i went ahead and created a hash for the api calls as a method of checking the software as a detection.

Sure this isn't a great detection method but it's about the best i could do right now - below is a list of the api calls made along with the generated hash + hash generation method
API Hash ID: 5daf34363d57d0d7cc20d390437a57951ea2282a0f67ba70e3babd0968ee955f

        'GetModuleFileNameW', 'LocalAlloc', 'Sleep', 'qsort', 'CertCloseStore', '__acrt_iob_func', 
        '__p__environ', '_access_s', '_mbtowc_l', 'LoadLibraryA', 'ExitProcess', 'SetProcessAffinityMask', 
        '_getch', '__daylight', '__setusermatherr', 'GetProcAddress', 'GetModuleHandleA', '_strtod_l', 
        '_aligned_free', 'GetUserObjectInformationW', 'CryptAcquireContextW', 'memchr', '_isctype_l', 
        'GetProcessWindowStation', 'GetVersion', 'WTSSendMessageW', 'FreeLibrary', '__p___argc', 'LocalFree', 
        'GetSystemTimeAsFileTime', 'SetThreadAffinityMask', '___lc_codepage_func', 'WSACleanup', 'GetProcessAffinityMask'


def generate_api_hash(api_calls):
    # Sort and concatenate API calls
    sorted_api_calls = sorted(api_calls)
    api_calls_str = ''.join(sorted_api_calls)

    # Generate hash ID
    hasher = hashlib.sha256()
    hasher.update(api_calls_str.encode('utf-8'))
    api_hash_id = hasher.hexdigest()

    return api_hash_id
