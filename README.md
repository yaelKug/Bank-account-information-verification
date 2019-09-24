"# Bank-account-information-verification" 


 function accountVerify(branch, account, codeBank) {
        var sum = 0;
        switch (codeBank) {
            case 10:
            case 13:
            case 34:
                sum = specificVerify(branch, account, 1098, 765432, true);
                if ((sum % 100) == 90 || sum % 100 == 72 || sum % 100 == 70 || sum % 100 == 60 || sum % 100 == 20)
                    return true;
                return false;
            case 12:
                sum = specificVerify(branch, account, 987, 654321, false);
                if (sum % 11 == 0 || sum % 11 == 2 || sum % 11 == 4 || sum % 11 == 6)
                    return true;
                return false;
            case 4:
                sum = specificVerify(branch, account, 987, 654321, false);
                if (sum % 11 == 0 || sum % 11 == 2)
                    return true;
                return false;
            case 11:
            case 17:
                sum = specificVerify(branch, account, 0, 987654321, false);
                if (sum % 11 == 0 || sum % 11 == 2 || sum % 11 == 4)
                    return true;
                return false;
            case 20:
                if (parseInt(branch) > 400) branch = (parseInt(branch) - 400).toString();
                sum = specificVerify(branch, account, 987, 654321, false);
                if (sum % 11 == 0 || sum % 11 == 2 || sum % 11 == 4)
                    return true;
                return false;
            case 31:
            case 52:
                sum = specificVerify(branch, account, 0, 987654321, false);
                if (sum % 11 == 0 || sum % 11 == 6)
                    return true;
                return false;
            case 9:
                sum = specificVerify(branch, account, 0, 987654321, false);
                if (sum % 10 != 0)
                    return false;
                return true;
            case 22:
                var temp = account.substring(accountMask.toString().length + 2);
                account = account.substring(0, accountMask.toString().length + 1);
                sum = specificVerify(branch, account, 0, 32765432, false);
                if (11 - sum % 11 != parseInt(temp))
                    return false;
                return true;
            case 46:
                sum = specificVerify(branch, account, 0, 987654321, false);
                if (sum % 11 == 0)
                    return true;
                else {
                    sum = specificVerify(branch, account, 987, 654321, false);
                    if (sum % 11 == 0)
                        return true;
                    else if ((branch == "192" || branch == "191" || branch == "183" || branch == "181" ||
                        branch == "178" || branch == "166" || branch == "154" || branch == "539" || branch == "505" ||
                        branch == "527" || branch == "516" || branch == "515" || branch == "507" || branch == "503") && sum % 11 == 2)
                        return true;
                    else
                        return false;
                }
        }
        return true;
    }
    
function specificVerify(branch, account, branchMask, accountMask, bll) {
        var sum = 0;
        var branchConvert = parseInt(branch), accountConvert;
        for (var i = 0; i <= 2; i++) {
            sum += (bll && branchMask == 10 ? 10 : (branchMask % 10)) * (branchConvert % 10);
            branchMask = Math.floor(branchMask /= 10);
            branchConvert = Math.floor(branchConvert /= 10);
        }
        if (bll) {
            sum += parseInt(account.substring(account.length - 2));
            account = account.substring(0, account.length - 2);
        }
        accountConvert = parseInt(account);
        for (var i = account.length; i > 0; i--) {
            sum += (accountMask % 10) * (accountConvert % 10);
            accountMask = Math.floor(accountMask /= 10);
            accountConvert = Math.floor(accountConvert /= 10);
        }
        return sum;
    }
    
