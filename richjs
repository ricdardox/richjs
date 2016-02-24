/* 
 * To change this license header, choose License Headers in Project Properties.
 * To change this template file, choose Tools | Templates
 * and open the template in the editor.
 */
/* 
 * To change this license header, choose License Headers in Project Properties.
 * To change this template file, choose Tools | Templates
 * and open the template in the editor.
 */

//Requiere de jquery
var richjs = {
    alert: 'alert',
    info: 'info',
    warning: 'warning',
    danger: 'danger',
    success: 'success',
    showMessage: function (data, selector) {
        var dataConfig = {
            type: 'info',
            message: ''
        };
        $.extend(dataConfig, data);
        $(selector).html('<div class="alert alert-' + dataConfig.type + '"><button type="button" class="close" data-dismiss="alert">&times;</button>' + dataConfig.message + '</div>');
    },
    isMessage: function (data, type) {
        try {
            if (data.type === type) {
                return true;
            }
        } catch (e) {
            return false;
        }
        return false;
    },
    /**
     * Muestra los errores de validación que manda el server a en el formulario
     * 
     * data': {}, 'formulario': '', 'limpiar': false
     * @param {type} config
     * @returns {undefined}
     */
    mostrarForm: function (config) {
        var configLocal = {
            'data': {}, 'formulario': '', 'limpiar': true
        };
        $.extend(configLocal, config);

        if (!richjs.isDefined(configLocal.limpiar)) {
            configLocal.limpiar = false;
        }
        var form = $(configLocal.formulario);
        var campos = form.serializeArray();
        var formAux = $();
        if (!campos.length) {
            formAux = $('<form></form>');
            formAux.append(form.clone());
            campos = formAux.serializeArray();
        }
        $.each(campos, function (index, a) {
            if (configLocal.data[a.name] !== undefined || configLocal.limpiar)
                form.find("#" + a.name).val(configLocal.data[a.name]);
        });
    },
    mostrarErrores: function (data) {
        $.each(data, function (iter, msg) {
            var id = iter + "-error";
            $('#' + id).remove();
            $('<label id="' + id + '" class="error val-peremdis" for="' + iter + '">' + msg + '</label>').insertAfter('#' + iter);
        });
    },
    getVarUrl: function (name) {
        var regexS = "[\\?&]" + name + "=([^&#]*)";
        var regex = new RegExp(regexS);
        var tmpURL = window.location.href;
        var results = regex.exec(tmpURL);
        if (results === null)
            return"";
        else
            return results[1];
    },
    getVarUrlParam: function (url, name) {
        var regexS = "[\\?&]" + name + "=([^&#]*)";
        var regex = new RegExp(regexS);
        var tmpURL = url;
        var results = regex.exec(tmpURL);
        if (results === null)
            return"";
        else
            return results[1];
    },
    isDefined: function (varField) {
        if (typeof (varField) !== 'undefined') {
            return true;
        } else {
            return false;
        }
    },
    validateFields: function (required) {
        var isOk = true;
        $.each($(required), function (i) {
            if ($(this).val() === '') {
                isOk = false;
                $(this).addClass('.rich_error_val');
                richjs.effect($(this));
            } else {
                $(this).removeClass('.rich_error_val');
            }
        });
        return isOk;
    },
    effect: function (selector, posEffect) {
        var position = 5;
        var vec = ["blind", "bounce", "clip", "drop", "fade", "shake", "explode"];
        if (richjs.isDefined(posEffect) && posEffect < vec.length) {
            position = posEffect;
        }
        $(selector).hide();
        $.each($(selector), function () {
            $(this).show(vec[position], null, 500);
        });
    },
    cargarSelectDependiente: function (config) {
        var lConfig = {
            'selIndependiente': '',
            'selDependiente': '',
            'url': '',
            'evento': true,
            'tipoEvento': 'change',
            'success': function (data) {
            }
        };
        $.extend(lConfig, config);
        var cargar = function (padre) {
            var select = $(lConfig.selDependiente);
            select.html('<option value="">Cargando...</option>');
            if (padre !== '') {
                richjs.sendServer({
                    'url': lConfig.url,
                    'data': {
                        'superior': padre,
                        '_token': $('input[name="_token"]').val()
                    },
                    'success': function (data) {
                        select.html('<option value="">Seleccione...</option>');
                        $.each(data, function (i, vec) {
                            select.append('<option value="' + vec.value + '">' + vec.tag + '</option>');
                        });
                        lConfig.success(data);
                    }
                });
            } else {
                select.html('<option value="">Seleccione...</option>');
                select.trigger(lConfig.tipoEvento);

            }
        };
        if (lConfig.evento) {
            $(lConfig.selIndependiente).on(lConfig.tipoEvento, function () {
                cargar($(this).val());
            });
        } else {
            cargar($(lConfig.seIndependiente).val());
        }

    },
    /**
     * Esta función se encarga de enviar las peticiones ajax al servidor
     * @param {type} parametros es el objecto con la configuración del ajax que se desea enviar
     * @returns {undefined}
     */
    sendServer: function (parametros) {
        /**
         * Configuración de la petición ajax
         * @type json
         */
        var configAjax = {
            'classicon': 'cargando32',
            'classiconshow': '.cargandomostrar',
            'url': 'no_definida',
            'method': 'POST',
            'data': {},
            'addData': {},
            'dataType': 'json',
            'success': function (data) {
                console.log('defectoResponse');
            },
            'error': function () {
                console.dir('errorResponse');
            }
        };
        $.extend(configAjax, parametros);
        $(configAjax.classiconshow).addClass(configAjax.classicon);
        $.ajax(configAjax).done(function (data) {
            $(configAjax.classiconshow).removeClass(configAjax.classicon);
        });
    }


};
