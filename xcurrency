/*!
 * money.js / fx() v0.1.3
 * Copyright 2011, Joss Crowcroft
 *
 * JavaScript library for realtime currency conversion and exchange rate calculation.
 *
 * Freely distributable under the MIT license.
 * Portions of money.js are inspired by or borrowed from underscore.js
 *
 * For details, examples and documentation:
 * http://josscrowcroft.github.com/money.js/
 */
function convertEl(e) {
    var t = accounting.unformat($(e).html());
    console.log("value" + t);
    var n = $.cookie("currency");
    console.log("target" + n), console.log("base" + gBase);
    var r = fx(t).from(gBase).to(n);
    console.log("converted: " + r);
    var i = "%s %v";
    $(e).hasClass("no_symbol") && (i = "%v"), $(e).html(accounting.formatMoney(r, {
        symbol: n,
        format: i,
        decimal: ".",  // decimal point separator
	thousand: ",",  // thousands separator
	precision : 2   // decimal places
    }))
}(function(e, t) {
    var n = function(e) {
        return new o(e)
    };
    n.version = "0.1.3";
    var r = e.fxSetup || {
        rates: {},
        base: ""
    };
    n.rates = r.rates, n.base = r.base, n.settings = {
        from: r.from || n.base,
        to: r.to || n.base
    };
    var i = n.convert = function(e, t) {
            if (typeof e == "object" && e.length) {
                for (var r = 0; r < e.length; r++) e[r] = i(e[r], t);
                return e
            }
            return t = t || {}, t.from || (t.from = n.settings.from), t.to || (t.to = n.settings.to), e * s(t.to, t.from)
        },
        s = function(e, t) {
            var r = n.rates;
            r[n.base] = 1;
            if (!r[e] || !r[t]) throw "fx error";
            return t === n.base ? r[e] : e === n.base ? 1 / r[t] : r[e] * (1 / r[t])
        },
        o = function(e) {
            typeof e == "string" ? (this._v = parseFloat(e.replace(/[^0-9-.]/g, "")), this._fx = e.replace(/([^A-Za-z])/g, "")) : this._v = e
        },
        u = n.prototype = o.prototype;
    u.convert = function() {
        var e = Array.prototype.slice.call(arguments);
        return e.unshift(this._v), i.apply(n, e)
    }, u.from = function(e) {
        var t = n(i(this._v, {
            from: e,
            to: n.base
        }));
        return t._fx = n.base, t
    }, u.to = function(e) {
        return i(this._v, {
            from: this._fx ? this._fx : n.settings.from,
            to: e
        })
    }, typeof exports != "undefined" ? (typeof module != "undefined" && module.exports && (exports = module.exports = n), exports.fx = n) : typeof define == "function" && define.amd ? define([], function() {
        return n
    }) : (n.noConflict = function(r) {
        return function() {
            return e.fx = r, n.noConflict = t, n
        }
    }(e.fx), e.fx = n)
})(this),
function(e, t) {
    function n(e) {
        return !!("" === e || e && e.charCodeAt && e.substr)
    }

    function r(e) {
        return c ? c(e) : "[object Array]" === h.call(e)
    }

    function i(e) {
        return "[object Object]" === h.call(e)
    }

    function s(e, t) {
        var n, e = e || {},
            t = t || {};
        for (n in t) t.hasOwnProperty(n) && null == e[n] && (e[n] = t[n]);
        return e
    }

    function o(e, t, n) {
        var r = [],
            i, s;
        if (!e) return r;
        if (l && e.map === l) return e.map(t, n);
        for (i = 0, s = e.length; i < s; i++) r[i] = t.call(n, e[i], i, e);
        return r
    }

    function u(e, t) {
        return e = Math.round(Math.abs(e)), isNaN(e) ? t : e
    }

    function a(e) {
        var t = f.settings.currency.format;
        return "function" == typeof e && (e = e()), n(e) && e.match("%v") ? {
            pos: e,
            neg: e.replace("-", "").replace("%v", "-%v"),
            zero: e
        } : !e || !e.pos || !e.pos.match("%v") ? n(t) ? f.settings.currency.format = {
            pos: t,
            neg: t.replace("%v", "-%v"),
            zero: t
        } : t : e
    }
    var f = {
            version: "0.3.2",
            settings: {
                currency: {
                    symbol: "$",
                    format: "%s%v",
                    decimal: ".",
                    thousand: ",",
                    precision: 2,
                    grouping: 3
                },
                number: {
                    precision: 0,
                    grouping: 3,
                    thousand: ",",
                    decimal: "."
                }
            }
        },
        l = Array.prototype.map,
        c = Array.isArray,
        h = Object.prototype.toString,
        p = f.unformat = f.parse = function(e, t) {
            if (r(e)) return o(e, function(e) {
                return p(e, t)
            });
            e = e || 0;
            if ("number" == typeof e) return e;
            var t = t || ".",
                n = RegExp("[^0-9-" + t + "]", ["g"]),
                n = parseFloat(("" + e).replace(/\((.*)\)/, "-$1").replace(n, "").replace(t, "."));
            return isNaN(n) ? 0 : n
        },
        d = f.toFixed = function(e, t) {
            var t = u(t, f.settings.number.precision),
                n = Math.pow(10, t);
            return (Math.round(f.unformat(e) * n) / n).toFixed(t)
        },
        v = f.formatNumber = function(e, t, n, a) {
            if (r(e)) return o(e, function(e) {
                return v(e, t, n, a)
            });
            var e = p(e),
                l = s(i(t) ? t : {
                    precision: t,
                    thousand: n,
                    decimal: a
                }, f.settings.number),
                c = u(l.precision),
                h = 0 > e ? "-" : "",
                m = parseInt(d(Math.abs(e || 0), c), 10) + "",
                g = 3 < m.length ? m.length % 3 : 0;
            return h + (g ? m.substr(0, g) + l.thousand : "") + m.substr(g).replace(/(\d{3})(?=\d)/g, "$1" + l.thousand) + (c ? l.decimal + d(Math.abs(e), c).split(".")[1] : "")
        },
        m = f.formatMoney = function(e, t, n, l, c, h) {
            if (r(e)) return o(e, function(e) {
                return m(e, t, n, l, c, h)
            });
            var e = p(e),
                d = s(i(t) ? t : {
                    symbol: t,
                    precision: n,
                    thousand: l,
                    decimal: c,
                    format: h
                }, f.settings.currency),
                g = a(d.format);
            return (0 < e ? g.pos : 0 > e ? g.neg : g.zero).replace("%s", d.symbol).replace("%v", v(Math.abs(e), u(d.precision), d.thousand, d.decimal))
        };
    f.formatColumn = function(e, t, l, c, h, d) {
        if (!e) return [];
        var m = s(i(t) ? t : {
                symbol: t,
                precision: l,
                thousand: c,
                decimal: h,
                format: d
            }, f.settings.currency),
            g = a(m.format),
            y = g.pos.indexOf("%s") < g.pos.indexOf("%v") ? !0 : !1,
            b = 0,
            e = o(e, function(e) {
                return r(e) ? f.formatColumn(e, m) : (e = p(e), e = (0 < e ? g.pos : 0 > e ? g.neg : g.zero).replace("%s", m.symbol).replace("%v", v(Math.abs(e), u(m.precision), m.thousand, m.decimal)), e.length > b && (b = e.length), e)
            });
        return o(e, function(e) {
            return n(e) && e.length < b ? y ? e.replace(m.symbol, m.symbol + Array(b - e.length + 1).join(" ")) : Array(b - e.length + 1).join(" ") + e : e
        })
    }, "undefined" != typeof exports ? ("undefined" != typeof module && module.exports && (exports = module.exports = f), exports.accounting = f) : "function" == typeof define && define.amd ? define([], function() {
        return f
    }) : (f.noConflict = function(n) {
        return function() {
            return e.accounting = n, f.noConflict = t, f
        }
    }(e.accounting), e.accounting = f)
}(this),
function(e) {
    typeof define == "function" && define.amd ? define(["jquery"], e) : typeof exports == "object" ? e(require("jquery")) : e(jQuery)
}(function(e) {
    function n(e) {
        return u.raw ? e : encodeURIComponent(e)
    }

    function r(e) {
        return u.raw ? e : decodeURIComponent(e)
    }

    function i(e) {
        return n(u.json ? JSON.stringify(e) : String(e))
    }

    function s(e) {
        e.indexOf('"') === 0 && (e = e.slice(1, -1).replace(/\\"/g, '"').replace(/\\\\/g, "\\"));
        try {
            return e = decodeURIComponent(e.replace(t, " ")), u.json ? JSON.parse(e) : e
        } catch (n) {}
    }

    function o(t, n) {
        var r = u.raw ? t : s(t);
        return e.isFunction(n) ? n(r) : r
    }
    var t = /\+/g,
        u = e.cookie = function(t, s, a) {
            if (s !== undefined && !e.isFunction(s)) {
                a = e.extend({}, u.defaults, a);
                if (typeof a.expires == "number") {
                    var f = a.expires,
                        l = a.expires = new Date;
                    l.setTime(+l + f * 864e5)
                }
                return document.cookie = [n(t), "=", i(s), a.expires ? "; expires=" + a.expires.toUTCString() : "", a.path ? "; path=" + a.path : "", a.domain ? "; domain=" + a.domain : "", a.secure ? "; secure" : ""].join("")
            }
            var c = t ? undefined : {},
                h = document.cookie ? document.cookie.split("; ") : [];
            for (var p = 0, d = h.length; p < d; p++) {
                var v = h[p].split("="),
                    m = r(v.shift()),
                    g = v.join("=");
                if (t && t === m) {
                    c = o(g, s);
                    break
                }!t && (g = o(g)) !== undefined && (c[m] = g)
            }
            return c
        };
    u.defaults = {}, e.removeCookie = function(t, n) {
        return e.cookie(t) === undefined ? !1 : (e.cookie(t, "", e.extend({}, n, {
            expires: -1
        })), !e.cookie(t))
    }
});
var gBase;
(function(e) {
    e.fn.xcurrency = function(t) {
        function s() {
            var t = e.cookie("currency");
            t === n && (e.removeCookie("currency"), e.removeCookie("xrate")), e(".xprice").each(function() {
                var r = accounting.unformat(e(this).html()),
                    i = t,
                    s = fx(r).from(n).to(i),
                    o = " %s%v",
               	    newsymbol = e('option[value="' + i + '"]').attr('data-sign');
                e(this).hasClass("no_symbol") && (o = "%v"), e(this).html(accounting.formatMoney(s, {
                    symbol: newsymbol,
                    format: o,
                    decimal: ".",  // decimal point separator
	            thousand: ",",  // thousands separator
	            precision : 2   // decimal places
                }))
            }), e(".xprice_options .xoption").each(function() {
                var t = e(this).attr("id"),
                    n = e(this).attr("value"),
                    r = e(this).children().html(),
                    i = "<option value=" + n + ">" + t + " - " + r + "</option>";
                e("select#option").append(e(i))
            }), e(".xprice_options").remove(), e(".unconverted").remove(), e(".converted").removeAttr("style")
        }

        function o() {
            e.ajax({
                type: "POST",
                url: "https://openexchangerates.org/api/latest.json?app_id=067e60ad38b5402fbfb8d79dcdaff439",
                success: function(e) {
                    e === null && r && console.log("success condition. null data returned: " + e)
                },
                error: function(e) {
                    e === null && r && console.log("error condition. null data returned: " + e)
                }
            })
        }

        function u() {
            e.ajax({
                type: "GET",
                url: "https://openexchangerates.org/api/latest.json?app_id=067e60ad38b5402fbfb8d79dcdaff439",
                async: !1,
                jsonpCallback: "jsonCallback",
                contentType: "application/json",
                dataType: "jsonp",
                success: function(t) {
                    r && console.log(t);
                    if (typeof fx != "undefined" && fx.rates) {
                        fx.rates = t.rates, fx.base = t.base, fx.timestamp = t.timestamp;
                        var n = new Date(e.now()),
                            i = new Date(fx.timestamp * 1e3),
                            u = (n - i) / 1e3 / 60;
                        u = parseInt(u, 10), r && (console.log("server date: " + i), console.log("current time: " + n), console.log("diff: " + u)), u > 300 && o(), s()
                    } else var a = {
                        rates: t.rates,
                        base: t.base
                    }
                },
                error: function(e) {
                    r && console.log(e.message)
                }
            })
        }
        var n = t.baseCurrency || "USD";
        gBase = n;
        var r = t.debug || !1;
        e(this).append('<option data-sign="$" value="' + n + '">' + n + "</option>");
        for (var i = 0; i < t.currencies.length; i++) e(this).append('<option data-sign="' + t.curSign[i] +'" value="' + t.currencies[i] + '">' + t.currencies[i] + "</option>");
        e.cookie("currency") && (e(this).val(e.cookie("currency")), u()), e(this).change(function() {
            var t = e(this).val();
            t === n ? e.removeCookie("currency", {
                path: "/"
            }) : e.cookie("currency", t, {
                expires: 1,
                path: "/"
            }), window.location.reload()
        })
    }
})(jQuery);


  (function($){    
    $(document).ready(function(){
        $('.currency_converter').xcurrency({
            baseCurrency: 'CAD',
            currencies: ["AUD", "CAD", "USD"],
            curSign: ["$", "$", "£", "€", "¥", "$"]
          
        });
      });
  })(jQuery)
